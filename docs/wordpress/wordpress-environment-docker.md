# How to Create a WordPress Environment Using Docker Compose

## Introduction

Using Docker Compose is a fast and efficient way to set up a WordPress environment with all the required software. 

## Important Terms
The following are important terms to understand when using Docker Compose: 

**Container** – an executable package that includes everything needed to run a piece of software. 
**Dockerfile** – a text file that defines all components that will be installed in a Docker environment.
**Image** – a template that contains instructions on how to build a Docker container.  
**Volume** – a dedicated folder on the host machine that stores data about the Docker environment. A volume lets you share data across multiple containers.

## Docker Installation
To install docker on your machine: 

1. Install the [Docker desktop client](https://www.docker.com/) for your platform (i.e. Windows, Mac, Linux). 
2.  Create a folder on your machine that will hold your Docker WordPress environment (for example, docker-local-wordpress).

## Create an Environment File
Your WordPress environment requires credentials that should not be committed to source control for security reasons. It’s a best practice to define the needed credentials in a separate .env file that your Docker Compose file can reference. 

In your docker project directory create a .env file with the following variables that will be used for your WordPress instance:

    WORDPRESS_DB_HOST=mariadb:3306
    WORDPRESS_DB_NAME=wordpress
    WORDPRESS_DB_USER=user
    WORDPRESS_DB_PASSWORD=userpassword

    MYSQL_ROOT_PASSWORD=rootpassword
    MYSQL_DATABASE=wordpress
    MYSQL_USER=mysqluser
    MYSQL_PASSWORD=mysqlpassword

    PHPMYADMIN_USER=phpmyadminuser
    PHPMYADMIN_PASSWORD=phpmyadminpassword

## Create a Docker Compose File

In the directory you created for your WordPress instance create a file called 
**docker-compose** (no file extension) and enter the following content:

    version: '3.9'

    services:
    db:
        image: mariadb:10.6
        container_name: mariadb
        restart: always
        environment:
        MYSQL_ROOT_PASSWORD: rootpassword
        MYSQL_DATABASE: wordpress
        MYSQL_USER: wordpress
        MYSQL_PASSWORD: wordpresspassword
        volumes:
        - db_data:/var/lib/mysql

    wordpress:
        image: wordpress:latest
        container_name: wordpress
        restart: always
        ports:
        - "8080:80"
        environment:
        WORDPRESS_DB_HOST: db:3306
        WORDPRESS_DB_USER: wordpress
        WORDPRESS_DB_PASSWORD: wordpresspassword
        WORDPRESS_DB_NAME: wordpress
        volumes:
        - wordpress_data:/var/www/html
        depends_on:
        - db

    phpmyadmin:
        image: phpmyadmin/phpmyadmin:latest
        container_name: phpmyadmin
        restart: always
        ports:
        - "8081:80"
        environment:
        PMA_HOST: db
        PMA_USER: root
        PMA_PASSWORD: rootpassword
        depends_on:
        - db

    volumes:
    db_data:
    wordpress_data:

**Note:** Update the version variable to the latest WordPress version.

Here's a version of the docker-compose file that allows phpmyadmin and wordpress to be on the same network:

    version: '3.9'

    services:
    db:
        image: mariadb:10.6
        container_name: mariadb
        restart: always
        environment:
        MYSQL_ROOT_PASSWORD: rootpassword
        MYSQL_DATABASE: wordpress
        MYSQL_USER: wordpress
        MYSQL_PASSWORD: wordpresspassword
        volumes:
        - db_data:/var/lib/mysql
        networks:
        - wpnet

    wordpress:
        image: wordpress:latest
        container_name: wordpress
        restart: always
        ports:
        - "8080:80"
        environment:
        WORDPRESS_DB_HOST: db:3306
        WORDPRESS_DB_USER: wordpress
        WORDPRESS_DB_PASSWORD: wordpresspassword
        WORDPRESS_DB_NAME: wordpress
        volumes:
        - wordpress_data:/var/www/html
        depends_on:
        - db
        networks:
        - wpnet

    phpmyadmin:
        image: phpmyadmin/phpmyadmin:latest
        container_name: phpmyadmin
        restart: always
        ports:
        - "8081:80"
        environment:
        PMA_HOST: db
        PMA_USER: root
        PMA_PASSWORD: rootpassword
        depends_on:
        - db
        networks:
        - wpnet

    volumes:
    db_data:
    wordpress_data:

    networks:
    wpnet:
        driver: bridge

To start Docker using your docker compose file, open a terminal from within your docker directory and run the following command: 

    docker-compose up -d

## Navigating to WordPress and PhpMyAdmin

Once your container is up and running, in Docker Desktop under Containers click the links under Ports column in your container to open the PhpMyAdmin console and WordPress console respectively.


After opening the WordPress console for the first time complete the WordPress installation wizard.
 
To stop the Docker container, open a terminal from within your Docker directory and run the following command:

    docker compose down

**Note:** After initially starting your container using the command line, containers can be stopped and started using the Docker Desktop UI.  