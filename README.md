deploy
======

Easy deploy Python WSGI apps

#### Authors

* Ondrej Sika, <http://ondrejsika.com/>, <ondrej@ondrejsika.com>

#### Sources

* project home - <https://github.com/sikaondrej/deploy/>
* main repository - <https://github.com/sikaondrej/deploy.git>
* pypi package - <https://pypi.python.org/pypi/deploy>
* lastest download version - <https://github.com/sikaondrej/deploy/archive/master.zip>

#### Donate project

<http://ondrejsika.com/donate/>

Installation
------------

### Depences

Need installed before install deploy

* nginx
* gunicorn
* supervisor
* git
* sudo
* node js (for CoffeeScript compilation)

### PIP installation

as root

    pip install deploy
    deploy-init


Create server
-------------

    deploy startserver appname "domain.com www.domain.com"

Application structure
---------------------

### wsgi
in project root must be file wsgi.py with variable application (wsgi application)

### pip requirements
if existst file requirements.txt in project root, auto install requirements to virtualenv in env dir

### post_update
post_update is executable file in app root, launched after git update. can be used for db migrations, etc.

Update via GIT
--------------

in production is branch master

    git remote add deploy git@server:appname.git
    git push deploy master

Edit server conf
----------------

opens vim with config file, then restart service

### nginx

    deploy serverconf "appname" nginx

### supervisor

    deploy serverconf "appname" supervisor

Restart server
--------------

restart only worker (supervisor), not nginx

    deploy restart "appname"


Remove server
-------------

remove server & create backup to BACKUP_DIR (default /var/deploy/backups). If you can remove app, fro security reason, type app name

    deploy remove "app"
    type app name [app]: app

if you can use remove in scripts, add paramenter -f (force)

    deploy remove "app" -f