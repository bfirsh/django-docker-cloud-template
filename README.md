# Django template for internal apps

This is a template for building internal company tools. It uses Google auth for signin and will check that you are authenticating with an account that is your company's domain so only employees can access the tool.

## Getting started

To get started (replace `myinternalapp` with the name of your app):

    $ docker run -it --rm -v "$PWD":/usr/src/app -w /usr/src/app django django-admin.py startproject --template https://github.com/bfirsh/django-internal-app-template/zipball/master myinternalapp
    $ cd myinternalapp

This readme file is now in your app's directory. You can delete this top bit and everything that follows is the start of your app's readme.


# {{ project_name }}

Description of {{ project_name }}.

## Running in development

Install Docker for Mac or Windows.

Create a new application in [Google's developer console](https://console.developers.google.com) and [enable the Google+ APIs](https://console.developers.google.com/apis/api/plus/overview). Go to the "Credentials" tab, then create some new OAuth credentials with these settings:

 * Application type: Web application
 * Authorized JavaScript origins: `http://www.127.0.0.1.xip.io:8000`
 * Authorized redirect URIs: `http://www.127.0.0.1.xip.io:8000/complete/google-oauth2/`

Save the client ID and client secret into a file called `.env`, along with a comma-separated list of Google Apps domains that you want to allow to log into the app (i.e. your company's domain):

```
SOCIAL_AUTH_GOOGLE_OAUTH2_KEY=...
SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET=...
SOCIAL_AUTH_GOOGLE_OAUTH2_WHITELISTED_DOMAINS=mycompany.com
```

We need a real domain in development for Google's OAuth. A service called xip.io can help us with this, but the app needs to be available on a predictable IP.

Run this to expose all your app's ports on 127.0.0.1:

    $ pinata set native/port-forwarding true

Do the initial database migration:

    $ docker-compose run web python manage.py migrate

Then to run the app:

    $ docker-compose up

Your app is now available at http://www.127.0.0.1.xip.io:8000

## Running in production

`docker-cloud.yml` is a Docker Cloud stack file.

First, you'll need to create a Google OAuth app similar to above, but using your app's public URL as the authorized URLs.

Next, upload `docker-cloud.yml` to Docker Cloud, filling in the environment section of your stack file with the OAuth credentials and `SECRET_KEY` with a random string.
