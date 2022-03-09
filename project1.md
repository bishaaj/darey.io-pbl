# STEP 3
## Project 1 - LAMP STACK IMPLEMENTATION (LAMP STACK) IN AWS

## Introduction
LAMP Stack is one of the popular open source software used for web application development. For web application to achieve expectation such as running smoothly, it has to include an operating system, a web server, a database, and a programming language.

Step 1 - INSTALLING APACHE AND UPDATING THE FIREWALL

`sudo apt update`

`sudo apt install apache2`

`sudo systemctl status apache2`
![apache-status](https://user-images.githubusercontent.com/34573768/157457806-1135d01a-bf85-4dc7-9925-1351693d86af.png)

The below link is a guide on how to install openssh on windows machine
- [Install openssh](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse)

The below link is a guide on how generate and manage ssh key
- [Generate openssh key_management](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_keymanagement)

My public ipaddress where apache2 default page is running
- [Apache2 Ubuntu Default Page up and running ](http://3.134.94.51/)

 `curl http://localhost:80`

 `curl http://127.0.0.1:80`
 ![apache-default-page1](https://user-images.githubusercontent.com/34573768/157460662-64a78c23-52de-45b4-9b35-57bf7c19b58f.png)
 
 `http://3.134.94.51/`
 ![apache-default-page2](https://user-images.githubusercontent.com/34573768/157460790-e5162c2f-c70e-4bf0-be39-a9656d73d843.png)
 
 ## Step 2 — INSTALLING MYSQL

`sudo apt install mysql-server`

`sudo mysql_secure_installation` Mysql installed
![mysql](https://user-images.githubusercontent.com/34573768/157461109-0928f75c-9db4-40b9-ac04-3fed088fd740.png)

## Step 3 — INSTALLING PHP

`sudo apt install php libapache2-mod-php php-mysql`

`php -v` PHP version installed
![php1](https://user-images.githubusercontent.com/34573768/157461626-dbfe703a-73a5-4244-9018-8d657acd0bb7.png)

## Step 4 — CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE

`sudo mkdir /var/www/projectlamp`

`sudo chown -R $USER:$USER /var/www/projectlamp`

`sudo vi /etc/apache2/sites-available/projectlamp.conf`

## Save and exit
`:wqa!`

`sudo ls /etc/apache2/sites-available`

`sudo a2ensite projectlamp`

`sudo a2dissite 000-default`

`sudo apache2ctl configtest`

`sudo systemctl reload apache2`

`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`
![apache1](https://user-images.githubusercontent.com/34573768/157461930-da8af11a-3195-4f8c-9ace-c21e61b225f5.png)

## STEP 5 — ENABLE PHP ON THE WEBSITE

`sudo vim /etc/apache2/mods-enabled/dir.conf`

`sudo systemctl reload apache2`

`vim /var/www/projectlamp/index.php` PHP page on website using my public ipaddress
![phpPage](https://user-images.githubusercontent.com/34573768/157462219-50a7500d-6ebf-4140-a057-7e79db5442a3.png)
