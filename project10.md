# STEP 20
# PROJECT 10: Load Balancer Solution With Nginx and SSL/TLS
## LOAD BALANCER SOLUTION WITH NGINX AND SSL/TLS
1. I started the project by spinning up a new Ubuntu 20.04 server with SSH security group. I configured TCP port 80 for HTTP protocol and added TCP PORT 443 for SSL/HTTPS protocol.
![port1](https://user-images.githubusercontent.com/34573768/160288011-aea77d8c-6ec0-4e63-8061-7d455ab97b8e.jpg)

2. I updated hosts file with my web 1 & 2 

![image](https://user-images.githubusercontent.com/34573768/160288074-2a62291d-6cda-4d8e-bc23-941f164d4428.png)

3. I update and installed sudo and Nginx with the following command

`sudo apt update && sudo apt install nginx`

I update this file `sudo vi /etc/nginx/nginx.conf` 

I restart the nginx and confirmed the running status with the following commands `sudo systemctl restart nginx && sudo systemctl status nginx`
![domain1](https://user-images.githubusercontent.com/34573768/160288236-f331af5e-c496-4f19-a23e-6b8b7d83843a.jpg)

# REGISTER A NEW DOMAIN NAME AND CONFIGURE SECURED CONNECTION USING SSL/TLS CERTIFICATES
1. I registered a domain name "www.toolingjosh.ga"
2. I read and follow the guides about how to create and Elastic Ip Address for a stable public ip address purposes. I 
   associate the Elastic Ip address to my Nginx-lb instance and update the A record with the DNS management of the domain
![domain1](https://user-images.githubusercontent.com/34573768/160288459-b6e5d6f8-a0cb-4dca-9ce9-83670cd36fe8.jpg)


4. I update the nginx.conf file to my domain name www.toolingjosh.ga 

5. I installed certbot for SSL certification application 

`sudo systemctl status snapd`

![snapd1](https://user-images.githubusercontent.com/34573768/160288649-1aac12a6-f535-4e79-ae95-2a778cb2f43f.jpg)

`sudo snap install --classic certbot`

`sudo ln -s /snap/bin/certbot /usr/bin/certbot`
`sudo certbot --nginx`

![certbot1](https://user-images.githubusercontent.com/34573768/160288615-1122c738-2089-4790-8c3e-55df9703cbf6.jpg)
![certbot2](https://user-images.githubusercontent.com/34573768/160288616-17751c67-f23e-4559-97a4-e41452a2b3b1.jpg)
![certbot3](https://user-images.githubusercontent.com/34573768/160288619-2d23af36-ae71-4c22-8692-9a1c42679c15.jpg)

I test my secure domain name and the outcome in the image below
![domain2](https://user-images.githubusercontent.com/34573768/160288698-2d4a064c-d13d-4007-9cd4-2ab889a035da.jpg)

Checked the SSL certificate information
![cert1](https://user-images.githubusercontent.com/34573768/160288728-2aa410b3-2d03-4602-9214-554820b9a107.jpg)
![cert2](https://user-images.githubusercontent.com/34573768/160288732-bdeee6be-31d0-4831-b381-135ddfe592ee.jpg)

I run this command to test certbot renewal `sudo certbot renew --dry-run`

I installed crontab to be able to add to add this line `* */12 * * *   root /usr/bin/certbot renew > /dev/null 2>&1` into it for SSL/TLS periodic renewal
![lb](https://user-images.githubusercontent.com/34573768/160288831-b530212f-68bf-49f5-a1b8-def5da9c6aaf.jpg) 











## TAKEAWAY
I took on project 10 yesterday night of which was going smoothly until i to the stage where i need to register a domain, so i checked out the project 10 video to see how it was done but i made a mistake of following the video to the end but i ended up on the wrong side because my nginx-lb threw error.
So i abandoned it and started afresh this afternoon, low and behold, it went so smoothly with minimal troubles and i got it right. I now know how to register a domain and not just a domain but a secured one too with elastic load balancer.

I have now learnt how to trust in my myself a bit more and have more confidence in myself.