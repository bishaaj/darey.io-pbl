# STEP 4

## PROJECT 2 - WEB STACK IMPLEMENTATION (LEMP STACK)

## Introduction
LEMP is another open source stack that can be used to serve a dynamic web pages and applications. While i used LAMP with apache2 webhost, i am going to use LEMP with Nginx and sql.

## Gitbash installed and connected to EC2-Instance
While LAMP configuration and implementation was mostly done using native Windows CMD, Powershell, i used gitbash for implementation of LEMP whilst there is no more difference between the tools, it certainly give me the experience and awareness that i can use gitbash to achieve same purpose.

`ssh -i "win-ec2.pem" ubuntu@ec2-3-134-94-51.us-east-2.compute.amazonaws.com` Gitbash server with ubuntu
![gitbash-server](https://user-images.githubusercontent.com/34573768/157470216-7f570303-78d7-4187-b428-fd04bf18a9a1.png)

## Step 1 – INSTALLING THE NGINX WEB SERVER

`sudo apt update`

`sudo apt install nginx`

`sudo systemctl status nginx`
![nginx1](https://user-images.githubusercontent.com/34573768/157470451-88236e49-b573-4284-aa97-7a25d972216f.png)

`curl http://localhost:80`
![nginx2](https://user-images.githubusercontent.com/34573768/157470918-6e510b25-5c70-4478-91af-d27bd1a4b145.png)

`http://18.220.119.20/` public ipaddress
![nginx3](https://user-images.githubusercontent.com/34573768/157471127-3e229852-cfd3-4299-bd11-24463ded3a65.png)

## Step 2 – INSTALLING MYSQL

`sudo apt install mysql-server`

`sudo mysql_secure_installation` mysql installed
![mysql1](https://user-images.githubusercontent.com/34573768/157471260-638206b3-eecb-41f9-9340-d11d59730a15.png)

## Step 3 – INSTALLING PHP

`sudo apt install php-fpm php-mysql` 

`php -v`  php version

![php1](https://user-images.githubusercontent.com/34573768/157471445-c4341f1a-af6c-48e5-8ca8-72f004533568.png)

## Step 4 – CONFIGURING NGINX TO USE PHP PROCESSOR

`sudo mkdir /var/www/projectLEMP`

`sudo chown -R $USER:$USER /var/www/projectLEMP`

`sudo nano /etc/nginx/sites-available/projectLEMP`

`sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/`

`sudo nginx -t` nginx status
![php2](https://user-images.githubusercontent.com/34573768/157471615-eba40757-b05f-4f51-9d98-08ffadd332a0.png)

`sudo unlink /etc/nginx/sites-enabled/default`

`sudo systemctl reload nginx`

`sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html`
![php4](https://user-images.githubusercontent.com/34573768/157472499-bfe37d07-a6fc-4875-85c1-184283e72727.png)

## Step 5 – TESTING PHP WITH NGINX

`sudo nano /var/www/projectLEMP/info.php`

`http://18.220.119.20/info.php`

![mysql3](https://user-images.githubusercontent.com/34573768/157472695-5f699b6f-04a7-4a75-a38c-e0322a1b3453.png)

## Step 6 – RETRIEVING DATA FROM MYSQL DATABASE WITH PHP (CONTINUED)

`sudo mysql`

`mysql> CREATE DATABASE 'example_database'`

`mysql>  CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password'`

`mysql> GRANT ALL ON example_database.* TO 'example_user'@'%'`

`mysql> exit`

`mysql -u example_user -p`

![mysql2](https://user-images.githubusercontent.com/34573768/157472889-4dd24074-946a-40b5-8060-dc4b5441ff76.png)

`SHOW DATABASES;`

![mysql3](https://user-images.githubusercontent.com/34573768/157473028-41fac80e-ef79-4440-9bc5-38d8933ca3e3.png)

`mysql> INSERT INTO example_database.todo_list (content) VALUES ("My first important item");`

`mysql> SELECT * FROM example_database.todo_list;`

![mysql4](https://user-images.githubusercontent.com/34573768/157473135-05f4f356-9c46-4a51-9732-d879a4101123.png)

`nano /var/www/projectLEMP/todo_list.php`

`http://18.220.119.20/todo_list.php`

![php5](https://user-images.githubusercontent.com/34573768/157473232-72881b8c-d1f2-437e-8f52-ea562eff46cd.png)

