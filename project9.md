# STEP - 19
# PROJECT 9: Continous Integration Pipeline For Tooling Website

## INSTALL AND CONFIGURE JENKINS SERVER
## STEP 1 - Install Jenkins server
I have launched a new EC2 instance ragged "Jenkins" and I update and intalled java JDK with the following commands

`sudo apt update`

`sudo apt install default-jdk-headless`

I installed Jenkins with the following commands

wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
    /etc/apt/sources.list.d/jenkins.list'

`sudo apt update`

`sudo apt-get install jenkins`

And I checked Jenkins status with this command

`sudo systemctl status jenkins`
![jenkins1](https://user-images.githubusercontent.com/34573768/160190596-c213f4b3-199f-48d3-86ba-9b79aff500ea.jpg)

I openned up default port 8080 to enable jenkins connection on webserver
![port8080](https://user-images.githubusercontent.com/34573768/160195180-e8ac8397-9fe9-41f6-8e90-c2ac82d12815.jpg)

I entered jenkins server public ipaddress http://18.170.43.156:8080/ in order to lunch and configure jenkins
![jenkins2](https://user-images.githubusercontent.com/34573768/160195415-6e56f548-d798-4cd3-982f-eaa3e91a04d8.jpg)

![jenkins3](https://user-images.githubusercontent.com/34573768/160195424-dd3969cc-2191-4603-8483-83cdcc3f5043.jpg)

## STEP 2 - Configure Jenkins to retrieve source codes from GitHub using Webhooks

1. I enabled webhooks in my GitHub repository settings by using my Jenkins public ipaddress in the github webhook payload
![webhook1](https://user-images.githubusercontent.com/34573768/160238156-d84db0c9-3cd4-4a68-a89a-1c0c8815267a.jpg)

2. I created a Freestyle project in Jenkins and i set the repository to connect with my project "darey.io-pbl"
![build1](https://user-images.githubusercontent.com/34573768/160238380-31097d55-67e0-4a46-bd59-e602b41fa2ce.jpg)

![build2](https://user-images.githubusercontent.com/34573768/160238387-8c8e2d45-b2ee-413a-9f7f-4b9b60f99963.jpg)

![build3](https://user-images.githubusercontent.com/34573768/160238394-698134b1-d9fa-49f5-aa5d-950e8b61f264.jpg) 

3. I added more configuration to the job in Jenkins by setting webhook to trigger Jenkins build job once a new code is pushed to git repository and also include "post build actions" in the configuration to achived all artifact files
![artifacts1](https://user-images.githubusercontent.com/34573768/160238667-7aec861f-6f8c-4771-a5e3-5f72061e8184.jpg)

`ls /var/lib/jenkins/jobs/tooling_github/builds/<build_number>/archive/`
![build6](https://user-images.githubusercontent.com/34573768/160238701-1e54d2ea-3aca-4fd8-ab27-98c048c90ddf.jpg)

# CONFIGURE JENKINS TO COPY FILES TO NFS SERVER VIA SSH
## Step 3 - Configure Jenkins to copy files to NFS server via SSH

1. I installed additional Jenkins plugin called "Publish Over SSH" to configure in Jenkins job
![ssh1](https://user-images.githubusercontent.com/34573768/160238850-11e4fd18-41d7-477a-be59-4af8b14d270b.jpg)

2. And then configured the SSH plugin in the iimage below
![ssh2](https://user-images.githubusercontent.com/34573768/160238882-71280485-6540-45ba-99be-e72abbc28eef.jpg)

3. After completing the configuration and i pushed updated code to git, Jenkins job was triggered but console output displayed an unstable outcome
![build8](https://user-images.githubusercontent.com/34573768/160238979-df145030-66a2-43c7-b54a-22a17ee1dfd9.jpg)

So i asked for help of what could be the reason and it became clear that there is need for ownership permission which i ran withis command
`sudo chown -R ec2-user:ec2-user /mnt`
![build9](https://user-images.githubusercontent.com/34573768/160239097-ca46484a-2418-4729-8f9f-5c5d531029ab.jpg)
## TAKEAWAY
It is good to always checked up on the next project just to have a clue of what it is. I almost terminate my nfs, db, web1 and 2 servers after completing project 8 but luckily i did not and i am glad about that.
Project 9 went smoothly as 8 with the only hicups comming from last steps but worked fine after i changed permission access.
