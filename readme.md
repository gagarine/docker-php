# Docker for PHP development (local machine)

Docker for PHP development on mac OSX. This was only tested with [Docker for MAC (beta)](https://docs.docker.com/docker-for-mac/).

By default docker-compose will launch 4 containers:
- nginx
- phpfpm
- db (mariadb)
- mailhog (it catch all email send by the phpfpm server)

Nginx and phpfpm are on debian 8 other are using smaller Alpine image.

You can change the configuration of nginx or phpfpm in Dockerfiles folder to meet you need.

This project use https://github.com/EugenMayer/docker-sync to sync your code with docker. This is a workaround to get (very) good performance until Docker for MAC shared volume is fixed.

## Start a new project

By default nginx is configured to serve ./app/web

Create this folder, add your code, then:

Start the synchronisation:

    $ docker-sync start

Create your containers:

    $ docker-compose up

Then check http://localhost:8080/

Emails are at: http://localhost:8025/

## Access DB on localhost

The DB port is exposed. To easily access it you can add this to your /etc/hosts

    db 127.0.0.1

