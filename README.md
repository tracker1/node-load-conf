node-load-conf
==============

Hierarchical configuration file loader for node.js


## Install

```
npm install load-conf
```

## Use

`.load(applicationName, [options])`

* applicationName - used to define the config path
* options (object) - optional parameters
  * watch (boolean) - watch the filesystem for changes
  * default (object) - default object to use for the configuration
    * applicationName's configuration is cached for the load-conf module
    * this means that only the *first* set of defaults to load will be applied

```
var conf = require("load-conf").load("APPNAME", { watch:true } /*actively watch for changes*/);
```

## Paths

The loader will look for and load the configuration files in the listed order, with each file overriding the prior file's settings.

`APPNAME` is the appname specified in the load command.
`NODE_ENV` is an environment variable (defaults to `development`)

Configuration Paths (global to user/active directory specific)

* `/etc/`
* `/etc/opt/`
* `%ALLUSERSPROFILE%/` - Windows environment variable
* `%APPDATA%/` - Windows environment variable
* `%LOCALAPPDATA%/` - Windows environment variable
* `~/Library/Application Support/` - OSX Common path
* `~/.config/` - LSB
* `./`

Each of application subpaths below will be appended in turn for the above configuration paths.

* `APPNAME.conf`
* `APPNAME.NODE_ENV.conf`
* `APPNAME/APPNAME.conf`
* `APPNAME/APPNAME.NODE_ENV.conf`

The resulting set...

* `/etc/APPNAME.conf`
* `/etc/APPNAME.NODE_ENV.conf`
* ...
* `./APPNAME/APPNAME.conf`
* `./APPNAME/APPNAME.NODE_ENV.conf`


## Methodology

The application files are merged together via [lodash's .merge](http://lodash.com/docs#merge) method.