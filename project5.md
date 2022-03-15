# STEP 12

# Project 5: Client/Server Architecture Using A MySQL Relational Database Management System

## CLIENT-SERVER ARCHITECTURE WITH MYSQL

`curl -Iv www.propitixhomes.com`

![server1](https://user-images.githubusercontent.com/34573768/158346201-95f0aa31-e098-472d-83f2-aa26feed58ab.png)

Create instance for mysql server and client

`Server A name - `mysql server``

`Server B name - `mysql client``

# db server

launch two instances (db & client server)

cd to the .pem dir `cd Downloads`

connect to db-server instance

update sudo `sudo apt update -y`

install mysql server `sudo apt install mysql-server`

enable mysql-server service `sudo systemctl enable mysql`

check mysql status `sudo systemctl status mysql` 
![server3](https://user-images.githubusercontent.com/34573768/158443474-efb9adb9-1e22-4285-98a3-dee82d418b41.png)

install db `sudo mysql_secure_installation` 
![db1](https://user-images.githubusercontent.com/34573768/158443537-b117784d-418d-4d40-9934-373af9edf6c7.png)

create user 

![db2](https://user-images.githubusercontent.com/34573768/158443851-6efa194b-3f3d-4d6f-8b41-834f7b1acece.png)

configure mysql to allow connection `sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf`

restart mysql server `sudo systemctl restart mysql`


# client server

launch and connect to client-server instance

update sudo `sudo apt update -y`

install mysql client `sudo apt install mysql-client -y`

configure port3306 
![port3306](https://user-images.githubusercontent.com/34573768/158443969-f9a71ac8-ff06-4e09-ac84-ea550cf6dce5.png)

connect to mysql server `sudo mysql -u remote_user -h 172.31.13.152 -p` 
![db3](https://user-images.githubusercontent.com/34573768/158444037-644f062b-5212-4508-b676-2c1a0ec93a76.png)

run sql commands `Show databases;` 

![db4](https://user-images.githubusercontent.com/34573768/158444091-5d1faa91-4c98-4d09-987c-4fe035f22258.png)

## Takeaway
The project docx isn't that great for an inexperience person like me. it is less details and give no clues of how to get going. The project video helps and improve the understanding of what needed to be done and how to do it. (Now i know you can create multiple instances in one goal for different purposes).
