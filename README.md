# udacity-linux-web-server
Linux Server Configuration - Configuring Linux Web Servers

Server IP - 13.229.120.57
SSH Port - 22

Web Site Address - http://13.229.120.57/



Installation steps

- Upgrade the server

- Enabled UFW firewall for ssh,www,ntp and 2222/tcp

- Create a new user - grader [password:grader]

- give sudo access to the new user 'grader'

- create ssh key for 'grader' -> ~/.ssh/authorized_keys.pub

- Install apache

- Download catalog application to /var/www/html/catalog folder via git

- Install mod_wsgi 

- Install pip

- Install flask,sqlalchemy,requests and oauth2cliento

- Install PostgreSQL 

- Create catalog database and catalog user

- install python-psycopg2

- Create database schema by running 'sudo python database_setup.py'

- Restart apache



