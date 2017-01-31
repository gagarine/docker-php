# Docker for PHP development on your local machine

Docker for PHP development on mac OSX with [Docker for MAC](https://docs.docker.com/docker-for-mac/).

This was tested with: Drupal 6 and 7 and Symfony but should works with any PHP applications.

By default docker-compose will launch 4 containers:
- nginx
- phpfpm (7.0 or 5.7)
- db (mariadb)
- mailhog ([MailHog](https://github.com/mailhog/MailHog) is configured to catch all email send by the phpfpm server)

Nginx and phpfpm are on debian 8. Other containers are using smaller alpine image.

You can change the configuration of nginx or phpfpm in Dockerfiles folder to meet you need.

This project use http://docker-sync.io/ to sync your code with docker. This is a workaround to get (very) good performance until Docker for MAC shared volume is fixed.

To install docker-sync:

    $ gem install docker-sync

## Start a new project

Copy every file of this repository in the root of your project.

By default nginx is configured to serve ./app/web. So, add your code in ./app/web, then:

In a terminal start the synchronisation and let it run:

    $ docker-sync start

In another terminal launch your containers:

    $ docker-compose up
    
All logs are redirected to the console, so you can quickly check nginx, php or mysql message.

Then load http://localhost:8080/ on your browser, you should see your PHP app.


## PHP version

Configurations for PHP7.0 and PHP5.6 are provided and work out of the box. You can chose the version you want by editing the docker-compose.yml file:

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
    
## Emails

All emails are caught (no email can go out accidentally) and stored in RAM. You can read emails on the MailHog web interface: http://localhost:8025/.

![Screenshot of MailHog web interface](https://raw.githubusercontent.com/mailhog/MailHog/master/docs/MailHog.png "MailHog web interface")
