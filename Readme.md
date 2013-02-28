Heroku buildpack: Buchner
=========================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for Buchner (or any other Python) apps, powered by [pip](http://www.pip-installer.org/).


Usage
-----

Example usage:

    $ ls
    Procfile  requirements.txt  web.py

    $ heroku create --buildpack git://github.com/heroku/heroku-buildpack-python.git

    $ git push heroku master
    ...
    -----> Python app detected
    -----> Installing runtime (python-2.7.9)
    -----> Installing dependencies using pip
           Downloading/unpacking requests (from -r requirements.txt (line 1))
           Installing collected packages: requests
           Successfully installed requests
           Cleaning up...
    -----> Discovering process types
           Procfile declares types -> (none)

You can also add it to upcoming builds of an existing application:

    $ heroku config:add BUILDPACK_URL=git://github.com/heroku/heroku-buildpack-python.git

The buildpack will detect your app as Python if it has the file `requirements.txt` in the root.

It will use Pip to install your dependencies, vendoring a copy of the Python runtime into your slug.

Installing Node.js
------------------

If you create a `node.json` file within the root of the project, the buildpack
will detect a Node.js dependency and install Node.js and npm.

This `node.json` file should be a facsimile of a `package.json` file as outlined
at http://package.json.nodejitsu.com/

Additional build related tasks
------------------------------

Sometimes you will have project specific tasks that need to be completed at
build time. This may be something like asset bundling or running migrations.

You may provide a `Buildfile` file in the root, which is essentially a shell
script to be run after all other standard build tasks are completed.

You may use the `$BUILD_DIR` variable to refer to the build directory within
this file.

Specify a Runtime
-----------------

You can also provide arbitrary releases Python with a `runtime.txt` file.

    $ cat runtime.txt
    python-3.4.3

Runtime options include:

- python-2.7.9
- python-3.4.3
- pypy-2.4.0 (unsupported, experimental)
- pypy3-2.4.0 (unsupported, experimental)

Other [unsupported runtimes](https://github.com/heroku/heroku-buildpack-python/tree/master/builds/runtimes) are available as well.
