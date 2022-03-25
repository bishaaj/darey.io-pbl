
# STEP 18
# PROJECT 8: Load Balancer Solution With Apache
## CONFIGURE APACHE AS A LOAD BALANCER

1. I created a new Ubuntu EC2 server named "Project-8-apache-lb" and i openned HTTP port 80 on it.

I installed apache2 on the server with the following steps

`sudo apt update

`sudo apt install apache2 -y

`sudo apt-get install libxml2-dev

#Enable following modules:

`sudo a2enmod rewrite`

`sudo a2enmod proxy`

`sudo a2enmod proxy_balancer`

`sudo a2enmod proxy_http`

`sudo a2enmod headers`

`sudo a2enmod lbmethod_bytraffic`

#Restart apache2 service

`sudo systemctl restart apache2`

I then checked apache2 with this command `sudo systemctl status apache2` to ensure that it is up and running
![apache1](https://user-images.githubusercontent.com/34573768/160076231-14a75f07-c10f-4add-ad61-112ea32cde25.jpg)

## Configure load balancing

I update apache2 config file with my webserver 1 & 2 private ipaddress with the following info

sudo vi /etc/apache2/sites-available/000-default.conf

#Add this configuration into this section <VirtualHost *:80>  </VirtualHost>

<Proxy "balancer://mycluster">

               BalancerMember http://172.31.43.151:80 loadfactor=5 timeout=1
               BalancerMember http://172.31.37.90:80 loadfactor=5 timeout=1
               ProxySet lbmethod=bytraffic
               # ProxySet lbmethod=byrequests

        </Proxy>

        ProxyPreserveHost On
        ProxyPass / balancer://mycluster/
        ProxyPassReverse / balancer://mycluster/

#Restart apache server

`sudo systemctl restart apache2`

I accessed my project8-load-balance public ipaddress with this url `http://35.176.61.22/index.php`
![apache2](https://user-images.githubusercontent.com/34573768/160076305-94658693-7d0d-4e6f-a59b-0a0522dc81c8.jpg)

So i logged by entering username and password and it displayed the below after logging in successfully
![apache3](https://user-images.githubusercontent.com/34573768/160076474-19b82309-324e-41d1-aa65-d438f49582ca.jpg)

I used this command `sudo tail -f /var/log/httpd/access_log` to unmount the /var/www/httpd that was mounted in project 7 and my webservers console display the image below after i refresh the public ipaddress
![lb1](https://user-images.githubusercontent.com/34573768/160076747-f4ed0827-c95d-4fc8-8ebc-500b77d8b142.jpg)

## Optional Step – Configure Local DNS Names Resolution
I update /etc/hosts file with the following info (The purpose of this to be able to handle and control multiple webservers with ease, there is need to configure local domain name resolution)

#Open this file on your LB server

sudo vi /etc/hosts

#Add 2 records into this file with Local IP address and arbitrary name for both of your Web Servers

"172.31.43.151 Web1"
"172.31.37.90 Web2"

I updated my apache2 load balancer config file by changing my webserver 1 & 2 private ipaddress to "web1 & web2"

"BalancerMember http://Web1:80 loadfactor=5 timeout=1"

"BalancerMember http://Web2:80 loadfactor=5 timeout=1"

Last command to check if the domain name resolution is working `curl http://Web1`
![curl1](https://user-images.githubusercontent.com/34573768/160078202-b5ba682e-4fa1-48dc-96c7-f17b5a95a97d.jpg)

![image](https://user-images.githubusercontent.com/34573768/160182165-096030f6-5645-410c-87d0-98f90e91cde0.png)



## TAKEAWAY