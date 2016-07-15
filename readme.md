# PHP docker

This project is a blueprint for php devlopement with docker.

By default docker-compose will launch 4 containers:
 - nginx
 - phpfpm
 - db (mariadb)
 - mailhog

Nginy is configured to serve ./app/web.

This project use https://github.com/EugenMayer/docker-sync to sync your code with docker.

## Start a new project

Create a local folder with app/web and put your code in it.

Start the syncronisation:

    $ docker-sync start

Create your containers:

    $ docker-compose up
