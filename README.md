# udacity-linux-web-server
Linux Server Configuration - Configuring Linux Web Servers

Server IP - 13.228.183.198

SSH Port - 2200

Web Site Address - http://13.228.183.198



# Installation steps

## Upgrade the server

sudo apt-get update

sudo apt-get upgrade


## Enabled UFW firewall for ssh,www,ntp and 2200/tcp

sudo ufw default deny incoming

sudo ufw default allow incoming

sudo ufw allow ssh

sudo ufw allow 2200/tcp

sudo ufw allow www

sudo ufw allow ntp

sudo ufw enable

#### REF
- Lesson 5 > Configuring Ports In UFW


## Create a new user - grader [password:grader]

sudo adduser grader

#### REF
- Lesson 5 > Creating A New User


## give sudo access to the new user 'grader'

sudo cp /etc/sudoers.d/90-cloud-init-users /etc/sudoers.d/grader

Change user name inside the file to 'grader' from 'ubuntu'

#### REF
- Lesson 5 > Introduction To Etc Sudoers

- Lesson 5 > Giving Sudo Access

## Copy authorized key for user 'grader'

sudo cp /root/.ssh/authorized_keys /home/grader/.ssh/authorized_keys

sudo chown grader:grader /home/grader/.ssh/authorized_keys

sudo chmod 644 /home/grader/.ssh/authorized_keys  

#### REF 
- https://discussions.udacity.com/t/where-to-create-ssh-key-pair-for-grader-using-the-ssh-keygen-tool/299527/2 (For copy key idea)

- https://aws.amazon.com/premiumsupport/knowledge-center/new-user-accounts-linux-instance/ ( For permissino Idea)
 

## Change SSH port to 2200

sudo nano /etc/ssh/sshd_config

sudo service ssh restart

#### REF
- https://sg.godaddy.com/help/changing-the-ssh-port-for-your-linux-server-7306


## Install apache

sudo apt-get install apache2

#### REF
- Lesson 6 > Installing Apache


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

#### REF
- Lesson 6 > Installing mod_wsgi


## Install pip

sudo apt-get install python-pip python-dev build-essential

#### REF
https://www.saltycrane.com/blog/2010/02/how-install-pip-ubuntu/


## Upgrade pip

sudo pip install --upgrade pip

#### REF
https://www.saltycrane.com/blog/2010/02/how-install-pip-ubuntu/


## Install flask,sqlalchemy,requests and oauth2client

sudo pip install flask sqlalchemy requests oauth2client

#### REF
http://www1.cmc.edu/pages/faculty/alee/cs40/penv/installFlaskOnWindows.html


## Install PostgreSQL 

sudo apt-get install postgresql

#### REF
- The Backend: Databases & Applications

## Login to PostgreSQL

sudo su - postgres

psql

#### REF
- The Backend: Databases & Applications


## Create catalog database and catalog user

CREATE DATABASE catalog;

CREATE USER catalog;

ALTER ROLE catalog WITH PASSWORD 'catalog';

GRANT ALL PRIVILEGES ON DATABASE catalog TO catalog;

\q

exit

#### REF
- The Backend: Databases & Applications


## install python-psycopg2

sudo apt-get install python-psycopg2

#### REF
- The Backend: Databases & Applications


## Create database schema

sudo python database_setup.py

#### REF
- The Backend: Databases & Applications


## Restart apache

sudo service apache2 restart


