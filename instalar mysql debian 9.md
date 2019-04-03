# INSTALATION MySQL Debian 9

**NOTE**: execute commands as a non-root user

## Run this commands
`sudo apt update`

`sudo apt upgrade`

## Download the file using wget
`wget https://dev.mysql.com/get/mysql-apt-config_0.8.10-1_all.deb`

dpkg is used to install, remove, and inspect .deb software packages. The -i flag indicates that we'd like to install from the specified file.

`sudo dpkg -i mysql-apt-config*`

`sudo apt update`

## Now we're ready to install:
`sudo apt install mysql-server`

MySQL should be installed and running now. Let's check using systemctl:

`sudo systemctl status mysql`

We connect to MySQL

`sudo mysql`

We change the password of the root user

`SET password FOR root@localhost = password('root');`

How to create a database

`CREATE DATABASE db_test;`

Show all users

`SELECT user FROM mysql.user;`

How to create user

`CREATE USER 'user_test'@'localhost' IDENTIFIED BY 'transmilenio';`

Show all databases

`SHOW DATABASES;`

Give user privileges on a database

`GRANT SELECT, INSERT, DELETE ON db_test.* TO 'user_test'@'localhost';`

Additional Information

ALL PRIVILEGES – grants all privileges to the MySQL user
CREATE – allows the user to create databases and tables
DROP - allows the user to drop databases and tables
DELETE - allows the user to delete rows from specific MySQL table
INSERT - allows the user to insert rows into specific MySQL table
SELECT – allows the user to read the database
UPDATE - allows the user to update table rows

Connect to user

`mysql -h localhost -u user_test -p`
