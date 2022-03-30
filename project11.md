# STEP 21
# PROJECT 11: Ansible – Automate Project 7 to 10
# ANSIBLE CONFIGURATION MANAGEMENT – AUTOMATE PROJECT 7 TO 10
## INSTALL AND CONFIGURE ANSIBLE ON EC2 INSTANCE
1. The first action i carried on this project was that i updated my Jenkins sserver tag to include ansible "jenkins-ansible"
2. Then i created a new repository named ansible-config-mgt" in my github account
3. I installed ansible on my jenkins-ansible server with `sudo apt install ansible`
   ![ansible1](https://user-images.githubusercontent.com/34573768/160894064-6c884940-9f0a-4168-b891-85e98e87467a.jpg)

4. I configured jenkins build job to save repository content everytime i changed it with the following steps
a. I created a freestyle project and linked it to Git in jenkins
b. I configured post build output pointed it to ssh
c. I configured a github webhook to jenkins to run a build job as soon as i pushed changes
d. I configured ssh connection with private key

5. I made changes to my README.md file and pushed it and it got picked up by jenkins build
![build1](https://user-images.githubusercontent.com/34573768/160893392-5cf47dec-f5aa-43f8-8736-094eb306bcbc.jpg)

`ls /var/lib/jenkins/jobs/ansible/builds/<build_number>/archive/`
![build2](https://user-images.githubusercontent.com/34573768/160893446-db6a7e94-4ebd-4601-8f5a-4e04d963c618.jpg)
## Step 2 – Prepare your development environment using Visual Studio Code
I have prepared the visual studio IDE and clone the "ansible-config-mgt" repository from github
![dev1](https://user-images.githubusercontent.com/34573768/160893542-d49e5b22-6841-4ca9-bb85-46b48bf68c20.jpg)
# BEGIN ANSIBLE DEVELOPMENT
![dev2](https://user-images.githubusercontent.com/34573768/160893662-3f6a86e9-c27a-4b9e-8c5e-dab5ed04d3a0.jpg)
## Step 4 – Set up an Ansible Inventory
![image](https://user-images.githubusercontent.com/34573768/160893858-e7b50568-364c-46cd-b86e-15bc7057a117.png)

1. After creating Ansible playbooks in VS code, i added my jenkins server into my local directory with these commands
`ssh-agent -s` and `ssh-add londonaz-ec2.pem`

2. I confirm the susccessful addition with `ssh-add -l`
![ssh1](https://user-images.githubusercontent.com/34573768/160895621-d8e20bbc-fe14-4a66-aff7-010c56d01017.jpg)

3. And ssh into my jenkins-ansible server `ssh -A ubuntu@18.171.34.169`
4. I created ansible playbooks and inventory files


## CREATE A COMMON PLAYBOOK
![git1](https://user-images.githubusercontent.com/34573768/160907113-0472ba87-90b5-4494-8218-5660123bd472.jpg)


# RUN FIRST ANSIBLE TEST
## Step 7 – Run first Ansible test
![git2](https://user-images.githubusercontent.com/34573768/160907665-d482b4ec-d3df-4eca-b203-a189fa89fbb3.jpg)
![build1](https://user-images.githubusercontent.com/34573768/160907132-8234dc61-2553-4199-acfe-049fd7e830ed.jpg)
![jenkins2](https://user-images.githubusercontent.com/34573768/160907179-dd174e38-84cd-439e-adfe-dd1040da049c.jpg)
![jenkins2](https://user-images.githubusercontent.com/34573768/160907938-608cdab5-2957-4d01-9ad0-5c3ad0857a2d.jpg)

I ran an ansible job with this code
`ansible-playbook -i /var/lib/jenkins/jobs/ansible/builds/7/archive/inventory/dev.yml /var/lib/jenkins/jobs/ansible/builds/7/archive/playbooks/common.yml`

![ansible3](https://user-images.githubusercontent.com/34573768/160907872-45285961-2807-4ae4-bc1c-14d7dc219c10.jpg)
![ansible4](https://user-images.githubusercontent.com/34573768/160907881-7ab0b98e-2c13-4632-a524-9d9fd3998d3c.jpg)

And my webswerver 1 & 2 including registered domain name displayed 
![web1](https://user-images.githubusercontent.com/34573768/160908492-cab30f8b-4b6a-4651-807f-b9c7c1f29673.jpg)