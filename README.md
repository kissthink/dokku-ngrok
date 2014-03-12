dokku-docker-options
========================

Basic docker options for dokku (https://github.com/progrium/dokku).

With a number of dokku plugins popping up to add options to docker it seemed silly to have one plugin per option type. This plugin allows you to add any type of docker option to an applications run/deploy.

Requirements
------------

Development version of dokku at or after https://github.com/progrium/dokku/commit/c77cbf1d3ae07f0eafb85082ed7edcae9e836147.

Installation
------------

```bash
$ cd /var/lib/dokku/plugins
$ sudo git clone https://github.com/dyson/dokku-docker-options.git docker-options
````

Usage
-----

```bash
$ dokku help
...
    docker-options <app>                            display docker options for an app
    docker-options:add <app> OPTIONS_STRING         add an option string an app
    docker-options:remove <app> OPTIONS_STRING      remove an option string from an app
...
````

Add some options

```bash
$ dokku docker-options:add myapp "-v /host/path:/container/path"
$ dokku docker-options:add myapp "-v /another/container/path"
$ dokku docker-options:add myapp "-link pgsql:db"
```

Check what we added

```bash
$ dokku docker-options myapp
-link pgsql:db
-v /host/path:/container/path
-v /another/container/path
```

Remove an option
```bash
$ dokku docker-options:remove myapp "-link pgsql:db"
```

Manual Usage
------------

In your applications folder (/home/dokku/app_name) create a file called DOCKER_OPTIONS.

Inside this file list one docker option per line*. For example:

```bash
-link pgsql:db
-v /host/path:/container/path
-v /another/container/path
```

The above example will result in the following options being passed to docker during deploy and docker run:

```bash
-link pgsql:db -v /host/path:/container/path -v /another/container/path
```

Move information on docker options can be found here: http://docs.docker.io/en/latest/reference/run/ .

_* Lines must end with a new line character. You can verify your line endings with:_ `cat -E PERSISTENT_STORAGE`
_and new line characters will be shown as $._

License
-------

MIT.