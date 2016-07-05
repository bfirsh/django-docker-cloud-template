# Django template for Docker Cloud

This is a template for Django applications that can be run with Docker Compose locally and Docker Cloud in production.

## Getting started

To get started (replace `myapp` with the name of your app):

    $ docker run -it --rm -v "$PWD":/usr/src/app -w /usr/src/app django django-admin.py startproject --template https://github.com/bfirsh/django-docker-cloud-template/zipball/master myapp
    $ cd myapp

This readme file is now in your app's directory. You can delete this top bit and everything that follows is the start of your app's readme.


# {{ project_name }}

Description of {{ project_name }}.

## Running in development

Install Docker for Mac or Windows.

Do the initial database migration:

    $ docker-compose run web python manage.py migrate

Then to run the app:

    $ docker-compose up

Your app is now available at http://localhost:8000

## Running in production

Upload `docker-cloud.yml` to Docker Cloud, filling in:

 - `SECRET_KEY` with a random string (run `openssl rand -base64 64` to generate)
 - `ALLOWED_HOSTS` with the hostname that the app is running on
