Sculpin Blog Skeleton
=====================

A skeleton for a Sculpin based blog.

Powered by [Sculpin](http://sculpin.io). =)


Features
--------

A very basic Sculpin based blog supporting the following features:

* Homepage with contact info and a list of blog posts
* Each blog post as a previous/next link and links to tag/category listings


Install
-------

Make sure you hhave composer installed

```bash
$ composer install
```

Build
-----

    php vendor/bin/sculpin generate --watch --server

Your newly generated clone of sculpin-blog-skeleton is now
accessible at `http://localhost:8000/`.


Previewing Development Builds
-----------------------------

By default the site will be generated in `output_dev/`. This is the location
of your development build.

To preview it with Sculpin's built in webserver, run either of the following
commands. This will start a simple webserver listening at `localhost:8000`.

### Using Sculpin's Internal Webserver

#### Generate Command

To serve files right after generating them, use the `generate` command with
the `--server` option:

    php vendor/bin/sculpin generate --server

To listen on a different port, specify the `--port` option:

    php vendor/bin/sculpin generate --server --port=9999

Combine with `--watch` to have Sculpin pick up changes as you make them:

    php vendor/bin/sculpin generate --server --watch


##### Server Command

To serve files that have already been generated, use the `serve` command:

    php vendor/bin/sculpin serve

To listen on a different port, specify the `--port` option:

    php vendor/bin/sculpin serve --port=9999


### Using a Standard Webserver

The only special consideration that needs to be taken into account for standard
webservers **in development** is the fact that the URLs generated may not match
the path at which the site is installed.

This can be solved by overriding the `site.url` configuration option when
generating the site.

    sculpin generate --url=http://my.dev.host/blog-skeleton/output_dev

With this option passed, `{{ site.url }}/about` will now be generated as
`http://my.dev.host/blog-skelton/output_dev/about` instead of `/about`.


Publishing Production Builds
----------------------------

When `--env=prod` is specified, the site will be generated in `output_prod/`. This
is the location of your production build.

    php vendor/bin/sculpin generate --env=prod

These files are suitable to be transferred directly to a production host. For example:

    php vendor/bin/sculpin generate --env=prod
    rsync -avze 'ssh -p 999' output_prod/ user@yoursculpinsite.com:public_html

If you want to make sure that rsync deletes files that you deleted locally on the on the remote too, add the `--delete` option to the rsync command:

    rsync -avze 'ssh -p 999' --delete output_prod/ user@yoursculpinsite.com:public_html

In fact, `publish.sh` is provided to get you started. If you plan on deploying to an
Amazon S3 bucket, you can use `s3-publish.sh` alongside the `s3cmd` utility (must be
installed separately).
