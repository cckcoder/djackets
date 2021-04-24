# Todo List

## Django Side

1. Install and setup (Django)

   1. `pip install django`
   1. `pip install django-rest-framework `
   1. `pip install django-cors-headers `
   1. `pip install djoser`
   1. `pip install pillow`

1. Setup settings.py install REST

```python
INSTALLED_APPS = [
    'rest_framework',
    'rest_framework.authtoken',
    'corsheaders',
    'djoser',
]

```

1. Then config urls

```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/v1/', include('djoser.urls')),
    path('api/v1/', include('djoser.urls.authtoken')),
]
```

1. makemigration `python3 manage.py makemigration`
1. migrate `python3 manage.py migrate`
1. create super user `python3 manage.py createsuperuser`
1. create product app `python manage.py startapp product`

## Vue Side

1. Install and setup (Vue)
   `npm install -g @vue/cli`

   1. create project with vue `vue create djackets_vue`

1. Include Font Awesome
1. Set up the base template
1. Create django app and models for products
1. Create serializer and views for the products
1. Create simple front page (latest products)
1. View a product
   1. Create viewset in Django
   1. Create vue page for showing product
   1. Add link to detail page
1. Setup opp Vuex / State

1. tools
   1. `npm install bulma-toast`

# Reference

https://github.com/SteinOveHelset/djackets_vue

# Server Setup (DigitalOcean)

1. `sudo apt install python3-pip python3-dev libpq-dev postgresql postgresql-contrib nginx`
1. `sudo apt install certbot python3-certbot-nginx`
1. setup postgresql
   1. `sudo -u postgres psql`
   1. create database `CREATE DATABASE djackets;`
   1. create user `CREATE USER djacketsuser WITH PASSWORD 'djacketspassword';`
   1. set encoding to utf8 `ALTER ROLE djacketsuser SET client_encoding TO 'utf8';`
   1. set up grant for user `GRANT ALL PRIVILEGES ON DATABASE djackets TO djacketsuser;`
   1. quit pgsql shell `\q`
1. setup python env
   1. `sudo -H pip3 install --upgrade pip`
   1. `sudo -H pip3 install virtualenv`
1. create project directory
   1. `mkdir -p /webapps/djackets`
1. create user group
   1. `sudo groupadd --system webapps`
1. add user
   1. `sudo useradd --system --gid webapps --shell /bin/bash --home /webapps/djackets djackets`
1. install pgsql python lib
   1. `pip install psycopg2-binary`
1. set permission `chown -R djackets:webapps .`
1. separate setting and manage for production
1. install gunicorn `pip install gunicorn`
1. config gunicorn

   1. `vi env/bin/gunicorn_start`
   1. `bash
      #!/bin/sh

      NAME='djackets_django'
      DJANGODIR=/webapps/djackets/djackets_django
      SOCKFILE=/webapps/djackets/env/run/gunicorn.sock
      USER=djackets
      GROUP=webapps
      NUM_WORKERS=3
      DJANGO_SETTINGS_MODULE=djackets_django.setting_production
      DJANGO_WSGI_MODULE=djackets_django.wsgi
      TIMEOUT=120

      cd $DJANGODIR
      source ../env/bin/activate
      export DJANGO_SETTINGS_MODULE=$DJANGO_SETTINGS_MODULE
      export PYTHONPATH=$DJANGODIR:$PYTHONPATH

      RUNDIR=$(dirname $SOCKFILE)
      test -d $RUNDIR || mkdir -p $RUNDIR

      exec ../env/bin/gunicorn ${DJANGO_WSGI_MODULE}:application \
      --name $NAME \
      --workers $NUM_WORKERS \
      --timeout $TIMEOUT \
      --user=$USER --group=$GROUP \
      --bind=unix:$SOCKFILE \
      --log-level=debug \
      --log-file=-
      `

   1. install supervisor `apt install supervisor`
   1. then `cd /etc/supervisor/conf.d`
   1. create file djackets.conf
   1. create supervisor log at env/logs

1. setup supervisor

   1. use `supervisorctl reread` to read djackets.conf
   1. then `supervisorctl update` to add djackets.conf
   1. then `supervisorctl status` to check djackets.conf is working

1. config NGINX
   1. go to dir `cd /etc/nginx/sites-available`
   1. create config file `vi apidjackets.codewizz.org`
   1. go to dir `/etc/nginx/sites-enabled/`
   1. make symbol link our config `ln -s ../sites-available/apidjackets.codewizz.org .`
   1. then `service nginx restart`
