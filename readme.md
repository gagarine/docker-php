# Docker for PHP development on your local machine

Docker for PHP development on mac OSX. This was only tested with [Docker for MAC](https://docs.docker.com/docker-for-mac/).

By default docker-compose will launch 4 containers:
- nginx
- phpfpm (7.0 or 5.7)
- db (mariadb)
- mailhog (it catch all email send by the phpfpm server)

Nginx and phpfpm are on debian 8. Other containers are using smaller alpine image.

You can change the configuration of nginx or phpfpm in Dockerfiles folder to meet you need.

This project use https://github.com/EugenMayer/docker-sync to sync your code with docker. This is a workaround to get (very) good performance until Docker for MAC shared volume is fixed.

## Start a new project

Copy every files of this repository in the root of your project.

By default nginx is configured to serve ./app/web. So, add your code in ./app/web, then:

In a terminal start the synchronisation and let it run:

    $ docker-sync start

In an other terminal launch your containers:

    $ docker-compose up
    
All logs are redirected to the console, so you can quickly check nginx, php or mysql message.

Then load http://localhost:8080/ on your browser, you should see your PHP app.

Emails are accessible on the MailHog web interface: http://localhost:8025/ their are only stored in RAM.

![Screenshot of MailHog web interface](https://raw.githubusercontent.com/mailhog/MailHog/master/docs/MailHog.png "MailHog web interface")


## PHP version

Configurations for PHP7.0 and PHP5.6 are provided and work out of the box. Chose the want to use by editing the docker-compose.yml file:

For PHP 5.7:

    phpfpm:
        build:
            context: ./Dockerfiles/phpfpm/5.7

For PHP 7.0:

    phpfpm:
        build:
            context: ./Dockerfiles/phpfpm/7.0
            

## Access DB on localhost

The DB port is exposed. To easily access it you can add this to your /etc/hosts

    db 127.0.0.1

