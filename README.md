dokku-ngrok
========================

Basic ngrok support for dokku (https://github.com/progrium/dokku).

Requirements
------------

Development version of dokku at or after https://github.com/progrium/dokku/commit/c77cbf1d3ae07f0eafb85082ed7edcae9e836147.

Installation
------------

```bash
$ cd /var/lib/dokku/plugins
$ sudo git clone https://github.com/gregpardo/dokku-ngrok.git ngrok
````

Usage
-----

```bash
$ dokku help
...
    ngrok <app>                            Display the status of ngrok configuration on an app
    ngrok:add <app> OPTIONS_STRING         Add an ngrok option string
    ngrok:remove <app> OPTIONS_STRING      Remove an ngrok option string
...
````

Add some options

```bash
$ dokku ngrok:add myapp "80"
$ dokku ngrok:add myapp "-subdomain=myappdb 54321"
```

Check what we added

```bash
$ dokku ngrok myapp
80
-subdomain=myappdb 54321
```

Remove an option
```bash
$ dokku ngrok:remove myapp "80"
```

Manual Usage
------------

In your applications folder (/home/dokku/app_name) create a file called NGROK_OPTIONS.

Inside this file list one docker option per line. For example:

```bash
80
-subdomain=myappdb 54321
```

You may also include comments (lines beginning with a #) and blank lines in the NGROK_OPTIONS file.

Move information on docker options can be found here: http://docs.docker.io/en/latest/reference/run/ .


License
-------

MIT.
