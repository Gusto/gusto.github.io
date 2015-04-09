---
permalink: v1/examples/authentication
layout: resource
title: Authentication Example
---

# Authentication

##  Safety First!

Due to the sensitive nature of payroll, all potential integrations must be vetted and approved by ZenPayroll.  To register an application, send an email to api@zenpayroll.com with a description of your company and use case.

## OAuth

### Getting Started

Authentication is done using [OAuth2](http://oauth.net/2/). Numerous libraries implementing the protocol can be found on the [OAuth2 homepage](http://oauth.net/2/).

Should you choose to implement your own flow, or if you just want to know more about what goes on behind the scenes, we'll walk through the basics of authenticating with ZenPayroll via OAuth. It can be a bit tricky - even with a library - so if you have questions at any point, please send us an email.

Outline:

- Direct user to authorize
- User authorizes application to access their information
- User redirected to partner site with authorization code
- Exchange authorization code for access/refresh token pair
- Make requests, always including the access token parameter
- Exchange refresh token for new access/refresh tokens

Here is the sample application information we'll use throughout:

```
  id:           bbb286ff1a4fe6b84742b0d49b8d0d65bd0208d27d3d50333591df71c45da519
  secret:       cb06cb755b868a819ead51671f0f7e9c35c7c4cbbae0e38bef167e0e4ba64ee6
  redirect_url: http://example.com/callback
```

### Authorization Code

> **Expiration Time:** 10 minutes
>
> **HTTP Method:** GET
>
> **URL:** https://zenpayroll.com/oauth/authorize
>
> **Parameters:**
>
> - `client_id` your client id
> - `redirect_uri` [percent-encoded](http://en.wikipedia.org/wiki/Percent-encoding/) url you submitted when signing up > for the ZenPayroll API. Should the user accept integration, the user will be returned to this url with the `code` parameter set to the authorization > code.
> - `response_type` the literal string `code`


The first step is a user authorizing your application to access their information on ZenPayroll. To do this, you'll create a link to ZenPayroll where they can approve access.

The link contains the parameters outlined above. For this sample application, the link would look something like this:

```html
  <a href="https://zenpayroll.com/oauth/authorize?client_id=bbb286ff1a4fe6b84742b0d49b8d0d65bd0208d27d3d50333591df71c45da519&redirect_uri=http%3A%2F%2Fexample.com%2Fcallback&response_type=code">Authorize with Zenpayroll</a>
```

On ZenPayroll, the user will be prompted to log in to their ZenPayroll account and authorize integration with your application for one or more of their companies.

After accepting, ZenPayroll will generate an authorization code and the user will be redirected to the redirect_uri with that code attached. In this case, the user will be sent to a url like this:

```
http://example.com/callback?code=51d5d63ae28783aecd59e7834be2c637a9ee260f241b191565aa10fe380471db
```

This parameter contains the authorization code that you will then use to obtain your first access token.

### Access Token

> **Expiration Time:** 2 hours.
>
> **HTTP Method:** POST
>
> **URL:** https://zenpayroll.com/oauth/token
>
> **Parameters:**
>
> - `client_id` - your client id
> - `client_secret` - your client secret
> - `redirect_uri` - the [percent-encoded](http://en.wikipedia.org/wiki/Percent-encoding/) url you submitted when signing up for the ZenPayroll API.
> - `code` - the code being exchanged for an access token. This should be the Authorization Code received above (`51d5d63ae28783aecd59e7834be2c637a9ee260f241b191565aa10fe380471db`.)
> - `grant_type` - this should be the literal string "authorization_code"

Next, you will make a server-side request to ZenPayroll with your authorization code to `https://zenpayroll.com/oauth/token` with the parameters outlined above. In this case, the request would look like this:

```
https://zenpayroll.com/oauth/token?client_id=bbb286ff1a4fe6b84742b0d49b8d0d65bd0208d27d3d50333591df71c45da519&client_secret=cb06cb755b868a819ead51671f0f7e9c35c7c4cbbae0e38bef167e0e4ba64ee6&redirect_uri=http%3A%2F%2Fexample.com%2Fcallback&code=51d5d63ae28783aecd59e7834be2c637a9ee260f241b191565aa10fe380471db&grant_type=authorization_code
```

That's a lot of information.

The `client_id`, `client_secret`, and `redirect_uri` are used to identify your application. We ensure that not only is it a valid application requesting a token, but also that it is the same application to which the included `code` was granted. The `code` matches the application to the user and the `grant_type` tells us what type of code is included.

Upon successful authentication, the response will look like this:

```javascript
  {
   "access_token": "de6780bc506a0446309bd9362820ba8aed28aa506c71eedbe1c5c4f9dd350e54",
   "token_type": "bearer",
   "expires_in": 7200,
   "refresh_token": "8257e65c97202ed1726cf9571600918f3bffb2544b26e00a61df9897668c33a1"
  }
```

The `access_token` should be included as a query parameter with every call to the API. Failure to include the `access_token` or using an expired token will result in a 401 response.

### Refresh Token

> **Expiration Time:** Never (invalid after one use)
>
> **HTTP Method** POST
>
> **URL** https://zenpayroll.com/oauth/token
>
> **Parameters:**
>
> - `client_id` your client id
> - `client_secret` your client secret
> - `redirect_uri` the percent-encoded url you submitted when signing up for the ZenPayroll API.
> - `refresh_token` the refresh_token being exchanged for an access token code.
> - `grant_type` this should be the literal string 'refresh_token'

Access tokens expire 2 hours after they are issued.

You may exchange your refresh token for a new access token once, making a request very similar to exchanging authorization code for an access token.

The only difference is that `code` is now `refresh_token` and `grant_type` is set to "refresh_token". Assuming you are refreshing the access token received in the previous section, here is the request you would make:

```
https://zenpayroll.com/oauth/token?client_id=bbb286ff1a4fe6b84742b0d49b8d0d65bd0208d27d3d50333591df71c45da519&client_secret=cb06cb755b868a819ead51671f0f7e9c35c7c4cbbae0e38bef167e0e4ba64ee6&redirect_uri=http%3A%2F%2Fexample.com%2Fcallback&refresh_token=8257e65c97202ed1726cf9571600918f3bffb2544b26e00a61df9897668c33a1&grant_type=refresh_token
```

The corresponding response, including both a fresh access token and a new refresh token, will look something like this:

```javascript
  {
   "access_token": "de6780bc506a0446309bd9362820ba8aed28aa506c71eedbe1c5c4f9dd350e54",
   "token_type": "bearer",
   "expires_in": 7200,
   "refresh_token": "8257e65c97202ed1726cf9571600918f3bffb2544b26e00a61df9897668c33a1"
  }
```


## API Token Authentication

There are certain endpoints that involve the application acting on behalf of
itself rather than a ZenPayroll user. For these, certified partners are granted
an API token. This token is included in the authorization HTTP header with the
`Token` scheme.

### Example

**HTTP Headers**

```
Content-Type: application/json
Authorization: Token bbb286ff1a4fe6b84742b0d49b8d0d65bd0208d27d3d50333591df71c45da519
```
