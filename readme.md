# PHP docker

This is a blueprint for php devlopement with docker on macosx.

By default docker-compose will launch 4 containers:
 - nginx
 - phpfpm (php5)
 - db (mariadb)
 - mailhog

Nginx and phpfpm are on debian 8 because I'm familair with this OS.

You can change the configuration of nginx or phpfpm in Dockerfiles folder to meet you need.

This project use https://github.com/EugenMayer/docker-sync to sync your code with docker.

## Start a new project

By default Nginy is configured to serve ./app/web

Create this folder, add your code, then:

Start the syncronisation:

    $ docker-sync start

Create your containers:

    $ docker-compose up


Then check http://localhost:8080/

Email are on: http://localhost:8025/
