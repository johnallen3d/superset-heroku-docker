# Superset on Heroku with Docker

Basic Superset deployment to Heroku with Docker (via `heroku.yml`).

## Why?

I tried a few of the [existing "one click installers"](https://github.com/RealScout/superset-on-heroku#realscout-superset-on-heroku) but all errored out. I'm personally more comfortable with containers so I went this route instead. 🤷

## Clone this repo

```sh
git clone git@github.com:johnallen3d/superset-heroku-docker.git
cd superset-heroku-docker
```

## Create Heroku App

Create a heroku application with [https://devcenter.heroku.com/articles/build-docker-images-heroku-yml#creating-your-app-from-setup](`heroku.yml` manifest support).

```sh
heroku update beta
heroku plugins:install @heroku-cli/plugin-manifest
heroku create YOUR_APP_NAME --manifest
git push heroku master
```

## Initialize Superset

```sh
# start up a shell session
heroku run bash --app YOUR_APP_NAME

# create an admin user
superset fab create-admin \
  --username admin \
  --firstname Superset \
  --lastname Admin \
  --email admin@superset.com \
  --password password1

# migrate db to latest
superset db upgrade

# optionally: load examples
superset load_examples

# setup roles
superset init
```

## Launch the application

```sh
heroku open
```

## Credit

These steps were cobbled together from a couple of sources, primarily:

* Official Docker Image - [https://hub.docker.com/r/apache/superset](https://hub.docker.com/r/apache/superset)
* This Deploy to Heroku setup - [https://github.com/RealScout/superset-on-heroku#realscout-superset-on-heroku](https://github.com/RealScout/superset-on-heroku#realscout-superset-on-heroku)
