# udacity-linux-web-server
Linux Server Configuration - Configuring Linux Web Servers

Server IP - 13.229.132.113

SSH Port - 2200

Web Site Address - http://13.229.132.113



# Installation steps

## Upgrade the server

sudo apt-get update
sudo apt-get upgrade


## Enabled UFW firewall for ssh,www,ntp and 2222/tcp

sudo ufw default deny incoming
sudo ufw default allow incoming
sudo ufw allow ssh
sudo ufw allow 2222/tcp
sudo ufw allow www
sudo ufw allow ntp
sudo ufw enable


## Create a new user - grader [password:grader]

sudo adduser grader

## give sudo access to the new user 'grader'

sudo cp /etc/sudoers.d/90-cloud-init-users /etc/sudoers.d/grader

Change user name to 'grader' from 'ubuntu'

## Create ssh key for 'grader' -> ~/.ssh/id_rsa.pub

su - grader [password:grader] 

ssh-keygen [key:grader]

## Change SSH port to 2200

sudo nano /etc/ssh/sshd_config

sudo service ssh restart

## Install apache

sudo apt-get install apache2

## Download catalog application to /var/www/html/catalog folder via git

sudo mkdir catalog

cd catalog

sudo git init

sudo git remote add origin https://github.com/ThetHlaing/udacity-catalog-aws.git

sudo git pull origin master



## Install mod_wsgi 

sudo apt-get install libapache2-mod-wsgi

sudo nano /etc/apache2/sites-enabled/000-default.conf

Add 'WSGIScriptAlias / /var/www/html/catalog/app.wsgi' at the end of the file

sudo apache2ctl restart



## Install pip

sudo apt-get install python-pip python-dev build-essential


## Upgrade pip

sudo pip install --upgrade pip


## Install flask,sqlalchemy,requests and oauth2client

sudo pip install flask sqlalchemy requests oauth2client


## Install PostgreSQL 

sudo apt-get install postgresql


## Login to PostgreSQL

sudo su - postgres

psql



## Create catalog database and catalog user

CREATE DATABASE catalog;

CREATE USER catalog;

ALTER ROLE catalog WITH PASSWORD 'catalog';

GRANT ALL PRIVILEGES ON DATABASE catalog TO catalog;

\q

exit



## install python-psycopg2

sudo apt-get install python-psycopg2


## Create database schema

sudo python database_setup.py


## Restart apache

sudo service apache2 restart


