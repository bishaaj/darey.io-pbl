# STEP - 14
# PROJECT 6: Web Solution With WordPress

## WEB SOLUTION WITH WORDPRESS

## Step 1 - Prepare a Web Server

create db and web server instances      
![server1](https://user-images.githubusercontent.com/34573768/158658154-a9531411-1bea-4a7c-8caa-5f3d7ab1cce9.png)

create 3 EBS vol of 10GiB     
![ebs1](https://user-images.githubusercontent.com/34573768/158658224-caaf3239-a84e-4bb4-b146-dcbb87c87cc2.png)

attach 3 EBS volume of 10GiB each to web-server      
![ebs2](https://user-images.githubusercontent.com/34573768/158658347-93c1bda5-a148-40a2-9ac1-c8d091f5c35f.png)

connect to server via gitbash terminal

inspect if the volume are attached successfully `lsblk`      
![ebs3](https://user-images.githubusercontent.com/34573768/158658409-54273d86-1281-443e-9aea-472a1094ad9c.png)

inspect /dev/ dir   `ls /dev/`       
![dir1](https://user-images.githubusercontent.com/34573768/158658544-5ae29d78-646d-4793-a3b1-834abd82571a.png)

check for free space `df -h`       
![dir2](https://user-images.githubusercontent.com/34573768/158658600-3f8eeab8-f83f-4325-91b3-3a37e9e3cffe.png)

create single partition `sudo gdisk /dev/xvdf`          
![part1](https://user-images.githubusercontent.com/34573768/158658796-3d308287-6142-4125-b29b-ed58f8254258.png)
![part2](https://user-images.githubusercontent.com/34573768/158658843-82cb186d-1849-42f3-8812-b8627c70d467.png)
![part3](https://user-images.githubusercontent.com/34573768/158658873-46a626ee-5d24-4afa-a4c1-be1bd47a292a.png)

install lvm2 `sudo yum install lvm2`      
![lvm2](https://user-images.githubusercontent.com/34573768/158658698-4a7ac436-7ae9-4add-aa6c-138172e25add.png)

check for available partitions `sudo lvmdiskscan`      
![lvm1](https://user-images.githubusercontent.com/34573768/158659031-23dedbda-f883-4d46-a3b0-c566b3721e78.png)

mark all the 3 disks as physical vol  

`sudo pvcreate /dev/xvdf1` 

`sudo pvcreate /dev/xvdg1`

`sudo pvcreate /dev/xvdh1`

inspect the 3 volumes `sudo pvs` 

![lvm3](https://user-images.githubusercontent.com/34573768/158659119-8bbe9b02-bb74-43e3-9efe-63bf4e3798e3.png)

create webdata-vg `sudo vgcreate webdata-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1`

inspect wddata-vg  

![vg1](https://user-images.githubusercontent.com/34573768/158659210-e031d985-eafe-4727-bc4a-fc069a5a9700.png)

create 2 logical volumes   

![lv1](https://user-images.githubusercontent.com/34573768/158659303-026f19ca-1850-4047-9c2f-a9f313753413.png)

`sudo lvcreate -n apps-lv -L 14G webdata-vg`

`sudo lvcreate -n logs-lv -L 14G webdata-vg`

verify the entire set up 

`sudo vgdisplay -v #view complete setup - VG, PV, and LV`

`lsblk`                    
![lv2](https://user-images.githubusercontent.com/34573768/158659388-7194d4cc-d5b8-4e6a-9ca4-697799898cd3.png)

format logical volume       
![lv3](https://user-images.githubusercontent.com/34573768/158659505-e825fd75-cda7-454d-a943-1dd19a1f0a2d.png)

`sudo mkfs -t ext4 /dev/webdata-vg/apps-lv`

`sudo mkfs -t ext4 /dev/webdata-vg/logs-lv`

creat /var/www/html directory 

`sudo mkdir -p /var/www/html`

`sudo mkdir -p /home/recovery/logs`

`sudo mount /dev/webdata-vg/apps-lv /var/www/html/`

backup all the files `sudo rsync -av /var/log/. /home/recovery/logs/`       
![files1](https://user-images.githubusercontent.com/34573768/158659708-53cb2358-2a7b-459e-b8f2-ec42049f2159.png)

mount /var/log on /logs-lv  `sudo mount /dev/webdata-vg/logs-lv /var/log`

restore log files
`sudo rsync -av /home/recovery/logs/. /var/log`

`sudo blkid`                 
![files2](https://user-images.githubusercontent.com/34573768/158659798-dada0565-f695-4829-adef-28656b7ad4b8.png)

`sudo mount -a`

`sudo systemctl daemon-reload`

verify setup `df -h`               
![mount1](https://user-images.githubusercontent.com/34573768/158659854-52482f8e-2af3-45a7-9b66-37b629780fbf.png)


## Step 2 - Prepare the Database Server

`sudo vgcreate database-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1`

`sudo lvcreate -n apps-lv -L 14G database-vg`
![db1](https://user-images.githubusercontent.com/34573768/158659927-5e1639da-acb6-42c2-8d81-0737f2a8bf41.png)

format logical volume `sudo mkfs -t ext4 /dev/database-vg/db-lv`

mount volume `sudo mount /dev/database-vg/db-lv /db` 
![db2](https://user-images.githubusercontent.com/34573768/158659982-721202e7-b19a-4764-a15d-5729729c6921.png)

`sudo vi /etc/fstab`

`sudo mount -a`

`sudo systemctl daemon-reload`       
![db3](https://user-images.githubusercontent.com/34573768/158660053-91e1b062-6b44-4610-a99d-08a05f99697e.png)


## Step 3 - Install WordPress on your Web Server EC2

## 1. update repo on db-server `sudo yum -y update`

## 2. install wget, apache & dependecies

`sudo yum -y install wget httpd php php-mysqlnd php-fpm php-json`


## 3. start apache

`sudo systemctl enable httpd`

`sudo systemctl start httpd`


## 4. to start PHP and it's dependency

`sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm`

`sudo yum install yum-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm`

`sudo yum module list php`

`sudo yum module reset php`

`sudo yum module enable php:remi-7.4`

`sudo yum install php php-opcache php-gd php-curl php-mysqlnd`

`sudo systemctl start php-fpm`

`sudo systemctl enable php-fpm`

`setsebool -P httpd_execmem 1`
![wordpress1](https://user-images.githubusercontent.com/34573768/158660469-c8d1b8e0-c1c5-4418-90ac-ce5db0c8daaf.png)

check php status `sudo systemctl status php-fpm` 
![php1](https://user-images.githubusercontent.com/34573768/158660195-f7ac7b7c-bd29-4d60-b6ea-fc71674b27c6.png)

## 5. Restart Apache

`sudo systemctl restart httpd`

check httpd status `sudo systemctl status httpd` 
![httpd1](https://user-images.githubusercontent.com/34573768/158660383-b76b6d98-df8d-461a-8705-573ba1049704.png)
![php2](https://user-images.githubusercontent.com/34573768/158661539-fbb9d775-3d9f-46b3-9345-61b6f492f356.png)

## 6. Download wordpress and copy wordpress to var/www/html

`mkdir wordpress`

`cd   wordpress`
 
`sudo wget http://wordpress.org/latest.tar.gz`
 
`sudo tar xzvf latest.tar.gz`

`sudo rm -rf latest.tar.gz`
 
`cp wordpress/wp-config-sample.php wordpress/wp-config.php`
 
`cp -R wordpress /var/www/html/`

## 7. Configure SELinux Policies

`sudo chown -R apache:apache /var/www/html/wordpress`
 `sudo chcon -t httpd_sys_rw_content_t /var/www/html/wordpress -R`
 `sudo setsebool -P httpd_can_network_connect=1`


## Step 4 — Install MySQL on your DB Server EC2

`sudo yum update`
`sudo yum install mysql-server`
`sudo systemctl restart mysqld`
`sudo systemctl enable mysqld`
![mysqld1](https://user-images.githubusercontent.com/34573768/158660912-60982701-7c63-4e7a-a319-fe0d76d52505.png)

## Step 5 — Configure DB to work with WordPress
`sudo mysql_secure_installation`

![db4](https://user-images.githubusercontent.com/34573768/158660952-99b45afa-bb96-41b8-8246-bb4b2180fe14.png)

`sudo mysql -u root -p`
CREATE USER `myuser`@`172.31.34.198` IDENTIFIED BY 'mypass';
GRANT ALL ON wordpresss.* TO 'myuser'@'172.31.34.198';
show databases;
select user, host from mysql.user;

![db5](https://user-images.githubusercontent.com/34573768/158661015-311f4a7e-1ac5-4407-8f69-9d7ada2334e9.png)
![db6](https://user-images.githubusercontent.com/34573768/158661038-9a513176-6266-48cd-947a-d4683b98542c.png)

`sudo vi /etc/my.cnf`

`vi wp-config.php`

## Step 6 — Configure WordPress to connect to remote database.

1. `sudo yum install mysql`

`sudo mysql -u admin -p -h <DB-Server-Private-IP-address>`

2. Verify if you can successfully execute SHOW DATABASES; command and see a list of existing databases 

![db7](https://user-images.githubusercontent.com/34573768/158661128-b2429a99-3b78-4e52-b2d9-d42253f971ab.png)

3. Change permissions and configuration so Apache could use WordPress:
4. 
`sudo mv /etc/httpd/conf.d/welcome.conf /etc/httpd/conf.d/welcome.conf_backup`

5. Try to access from your browser the link to your WordPress 

'http://13.40.235.126/wp-admin/install.php`

![wp1](https://user-images.githubusercontent.com/34573768/158661234-5e2fa235-e81d-499d-bdf1-345e79fc6474.png)
![wp2](https://user-images.githubusercontent.com/34573768/158661249-4c1afc19-de08-4b8c-8a63-c15632151d3e.png)
![wp3](https://user-images.githubusercontent.com/34573768/158661261-a1ffbc84-c5df-4b1c-bd0e-97a4ca1e399d.png)
