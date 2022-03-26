# STEP 17 
# PROJECT 7: Devops Tooling Website Solution
## DEVOPS TOOLING WEBSITE SOLUTION

# STEP 1 - PREPARE NFS SERVER
## Step 1 - Prepare NFS Server
1. Spin up a new EC2 instance with RHEL Linux 8 Operating System.

2. Based on your LVM experience from Project 6, Configure LVM on the Server.

create nfs, db and 3 web server instances      
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

create 3 logical volumes   

![lv1](https://user-images.githubusercontent.com/34573768/158659303-026f19ca-1850-4047-9c2f-a9f313753413.png)

`sudo lvcreate -n lv-apps -L 9G webdata-vg`

`sudo lvcreate -n lv-logs -L 9G webdata-vg`

`sudo lvcreate -n lv-opt -L 9G webdata-vg`

verify the entire set up 

`sudo vgdisplay -v #view complete setup - VG, PV, and LV`

`lsblk`                    
![lv2](https://user-images.githubusercontent.com/34573768/158659388-7194d4cc-d5b8-4e6a-9ca4-697799898cd3.png)

Format logical volume       
![lv3](https://user-images.githubusercontent.com/34573768/158659505-e825fd75-cda7-454d-a943-1dd19a1f0a2d.png)

`sudo mkfs -t xfs /dev/webdata-vg/lv-apps`

`sudo mkfs -t xfs /dev/webdata-vg/lv-logs`

`sudo mkfs -t xfs /dev/webdata-vg/lv-opt`

3 logical volumes mounted unto mount directory

`sudo mount /dev/webdata-vg/lv-apps /mnt/apps`

`sudo mount /dev/webdata-vg/lv-logs /mnt/logs`

`sudo mount /dev/webdata-vg/lv-opt /mnt/opt`

## 4. Install NFS server, configure it to start on reboot and make sure it is u and running
The following commands update, install, start, enable and checked nfs-server.service running state

`sudo yum -y update`

`sudo yum install nfs-utils -y`

`sudo systemctl start nfs-server.service`

`sudo systemctl enable nfs-server.service`

`sudo systemctl status nfs-server.service`

## 5. Subnet cidr ipv4 address
Webserver 1 to 3 were lunched within the same subnet and the subnet cidr was used to connect to NFS server so that all the servers an communicate together using a designated ports

The following commands was used to change ownership and read, write and execute permission

`sudo chown -R nobody: /mnt/apps`

`sudo chown -R nobody: /mnt/logs`

`sudo chown -R nobody: /mnt/opt`

`sudo chmod -R 777 /mnt/apps`

`sudo chmod -R 777 /mnt/logs`

`sudo chmod -R 777 /mnt/opt`

`sudo systemctl restart nfs-server.service`

## 6. port used by NFS
![nfs5](https://user-images.githubusercontent.com/34573768/159999370-c34bb447-e93c-45f1-aed4-56e5297eda19.jpg)

## NFS security inbound rules configuration
![image](https://user-images.githubusercontent.com/34573768/159999779-63e08fba-3bf4-4cd5-98cb-8ebb570555a5.png)


# STEP 2 - CONFIGURE THE DATABASE SERVER

Database server was configured using the experience learn in previous project but on this occassion, permission was given to webaccess to do anything on webserver subnet cidr address
![db1](https://user-images.githubusercontent.com/34573768/160000602-4f163adc-68d4-4b8d-b5f4-efabfef30b3f.jpg)

## Step 3 — Prepare the Web Servers

`sudo yum install nfs-utils nfs4-acl-tools -y`

`sudo mkdir /var/www`
`sudo mount -t nfs -o rw,nosuid 172.31.41.118:/mnt/apps /var/www`

Files created in any of the three webservers can be seen in another server
![image](https://user-images.githubusercontent.com/34573768/160011038-e3e58ffe-1d86-40a7-bee2-db071f47cf45.png)

![image](https://user-images.githubusercontent.com/34573768/160011466-da0cc71b-ffa2-40cb-9f51-6d18ea685f8a.png)

Edit fstab config `sudo vi /etc/fstab`

Update it with `172.31.41.118:/mnt/apps /var/www nfs defaults 0 0`

## Install Remi’s repository, Apache and PHP
`sudo yum install httpd -y`

`sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm`

`sudo dnf install dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm`

`sudo dnf module reset php`

`sudo dnf module enable php:remi-7.4`

`sudo dnf install php php-opcache php-gd php-curl php-mysqlnd`

`sudo systemctl start php-fpm`

`sudo systemctl enable php-fpm`

`sudo setsebool -P httpd_execmem 1`
![httpd1](https://user-images.githubusercontent.com/34573768/160002040-4fcc0027-9650-4d94-b846-93ae6929cdb7.jpg)

copied tooling source into html directory `sudo cp -R html/. /var/www/html`

I forked git repository for tooling source database and i deployed the code to webserver database.
![db2](https://user-images.githubusercontent.com/34573768/160002116-876eb2f4-9263-4c52-87f9-7324d7777140.jpg)

I update `sudo vi /var/www/html/functions.php` to read `mysql -h 172.31.43.26 -u <webaccess> -p <password> < tooling-db.sql`

I run webserver public ipaddress `http://13.40.108.171/index.php` 
![web8](https://user-images.githubusercontent.com/34573768/160002892-5cac1924-47b3-4cfc-b4e0-5dd0a11d09d8.jpg)


I logged in using the credential from the database
![admin](https://user-images.githubusercontent.com/34573768/160002969-bd8aef3c-a7fd-4837-abb2-7678e16385c4.jpg)

![image](https://user-images.githubusercontent.com/34573768/160178172-4905aa1e-9e7a-45ed-bb37-d3814ad99a9f.png)

## TAKEAWAY
Project 7 is a very good hands on which was very engaging from the beginning to the end. It does have some brain thinking aspect which could be easily picked out with concentration and could be very difficult to detect also and i experienced the later.
Project 7 taught to not just read up about instruction and guides but to also imagine or visualise what its going to look like and the expected result, this will help in guiding one in the right direction. Why did i said this?
My first attempt at project 7, i was on the last step which i only need to login but i didn't know so i thought to myself that i've got it all wrong and i had start all over again and this time around, i got it over the line.

I love the exposure of configuring multiple servers to achieve one goal.