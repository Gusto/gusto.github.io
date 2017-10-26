docs.gusto.com
====================

This is where API documentation for versions 1 and 2 of the Gusto API is housed.

Running
====================

This project is built on Jekyll, a Ruby gem that transforms markdown
into static HTML. After cloning this repository, run:

`bundle`

This installs all dependencies. Next, run the server with:

`bundle exec jekyll serve`

This will startup an instance of the documentation server, which is accessible at `http://127.0.0.1:4000/`.

The server will automatically regenerate HTML when you save changes to markdown, so there's no need to restart it as you develop. Just refresh the page.

Deploying
====================
Simply merge your feature branch into `master`. Everything else will happen automagically.