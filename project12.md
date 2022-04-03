# STEP 22
# PROJECT 12 - Ansible Refactoring, Assignments and Imports

## ANSIBLE REFACTORING AND STATIC ASSIGNMENTS (IMPORTS AND ROLES)
## Step 1 – Jenkins job enhancement
I started this project by creating a new directory on jenkins-ansible server `sudo mkdir /home/ubuntu/ansible-config-artifact`

![artifacts1](https://user-images.githubusercontent.com/34573768/161428536-fdbfb960-f2e0-4158-a585-bce8160f978a.jpg)

I change the permision to enable write access `sudo chmod -R 0777 /home/ubuntu/ansible-config-artifact`

To be able to copy artifact into a new folder, i added a new plugin "Copy Artifact" in Jenkins

![jenkins1](https://user-images.githubusercontent.com/34573768/161427666-aa86611b-8fbe-43b1-a999-8f6011fa32cd.jpg)

I create a new jenkins job titled "Save_artifact" and configured it to be trigger by 'ansible' and test the setup below

![jenkins2](https://user-images.githubusercontent.com/34573768/161427705-81d23145-0697-4de4-a317-df95c59d4121.jpg)

![jenkins3](https://user-images.githubusercontent.com/34573768/161427708-e154fe6a-230b-4767-b5d6-d3e5e026cd3a.jpg)
# REFACTOR ANSIBLE CODE BY IMPORTING OTHER PLAYBOOKS INTO SITE.YML
## Step 2 – Refactor Ansible code by importing other playbooks into site.yml
I created a new branch named "refactor" and ensure it has latest codes fom master branch

I added a new file 'site.yml' into playbooks directory

I created another directory "static-assigments" in the root of 'ansible-config-mgt' 

I moved 'common.yml' file into it

I copied 'common.yml' file into 'site.yml' file 

![image](https://user-images.githubusercontent.com/34573768/161428058-c4cc0ffc-df06-46b7-97a8-55d63045f425.png)

![image](https://user-images.githubusercontent.com/34573768/161428095-9e691756-cfbc-403a-bee0-fd3b0b126d41.png)

I created a new yaml file 'common-del.yml' which i configured to remove and delete wireshark and to confirm absence of wireshark.

I run the playbook against dev.yml with this command `sudo ansible-playbook -i /home/ubuntu/ansible-config-mgt/inventory/dev.yml /home/ubuntu/ansible-config-mgt/playbooks/site.yaml` and i got error in the image below

![ansible1](https://user-images.githubusercontent.com/34573768/161428269-e862b037-2eb5-4b58-8058-ee17e3bf246f.jpg)

## Solution
After so much troubleshooting and support from the team, three changes were made

I added nfs, db, web 1 & 2 and Nginx-lb private ipaddress to jenkins-ansible server file `/etc/ansible/hosts` 

I removed `sudo` from the ansible-playbook run command 

I replaced `ansible-config-mgt` with `ansible-config-artifact` in the run command and the result is below

![ansible2](https://user-images.githubusercontent.com/34573768/161428524-e0ddc182-c063-4e24-95d2-7b9859438aaf.jpg)
# CONFIGURE UAT WEBSERVERS WITH A ROLE ‘WEBSERVER’
## Step 3 – Configure UAT Webservers with a role ‘Webserver’
I started by spining up two new RHEL 8 linux servers and i named it 'web1-uat and web2-uat' and stopped other servers

![server1](https://user-images.githubusercontent.com/34573768/161429357-7ebe41ea-1938-4e62-bdcb-c957b5f1712e.jpg)

I added necessary security group to it such as port 22, 80 and 443

I added web1-uat and web2-uat private ipaddress to jenkins-ansible host file /etc/ansible/hosts'

I cd into ansible-config-mgt in jenkins-ansible server and i create a new directory named 'roles'

I cd into roles directory and i installed 'webserver' with this command `ansible-galaxy init webserver`

![file1](https://user-images.githubusercontent.com/34573768/161428954-109a8f1c-966a-4c03-9802-5986715112bf.jpg)

I made modification to webserver by using `rm -r tests vars files`

![file2](https://user-images.githubusercontent.com/34573768/161428964-be0f6c7c-88ce-495e-8d16-c24fda035fdd.jpg)

I update uat.yml file in the inventory directory

![image](https://user-images.githubusercontent.com/34573768/161429066-c89b2950-67e7-4b04-b0f4-2364440bb23a.png)

I uncomment role path in `/etc/ansible/ansible.cfg` and i added my file path to it `/home/ubuntu/ansible-config-artifact/roles`

I install and configured httpd on web1-uat & web2-uat with the following commands `sudo apt install httpd -y && sudo systemctl start httpd` and i then verified httpd status with `sudo systemctl status httpd`

![image](https://user-images.githubusercontent.com/34573768/161431469-f7e48ac0-a842-4ac1-9c87-b08fc5827fdf.png)

I cloned tooling from my repository using https url

![image](https://user-images.githubusercontent.com/34573768/161429282-d02993d6-7d8e-481e-af1b-178dbd53625a.png)

I update the main.yml file on webservers
# REFERENCE WEBSERVER ROLE
## Step 4 – Reference ‘Webserver’ role
created a new file `uat-webservers.yml` inside static-assignment directory

I also copy `uat-webservers.yml` into 'site.yml'

![image](https://user-images.githubusercontent.com/34573768/161429548-66e19efb-9fef-48e3-866f-5590718b1425.png)
## Step 5 – Commit & Test
I commit my configurations, reviewed and merged it to master branch

![git1](https://user-images.githubusercontent.com/34573768/161429589-3703a699-c57a-424d-a626-6a977ae409a3.jpg)

And I run the ansible-playbook command against uat `ansible-playbook -i /home/ubuntu/ansible-config-artifact/inventory/uat.yml /home/ubuntu/ansible-config-artifact/playbooks/site.yml`

![output1](https://user-images.githubusercontent.com/34573768/161429702-7c23ad64-7344-41f0-ad83-b49c020814f2.jpg)

It failed to find my web1-uat and web2-uat, so i update the uat.yml and uat-webservers.yml host to have the same name

![output2](https://user-images.githubusercontent.com/34573768/161429767-bfb97763-a20a-4819-95cc-f12e8bad89e2.jpg)

I made a conviguration change and works fine compared to above images

![image](https://user-images.githubusercontent.com/34573768/161431050-ba59675b-3084-4229-b2ca-1a38100a4e03.png)

And the web1-uat and web2-uat public ipaddress displayed 

![uat-web1](https://user-images.githubusercontent.com/34573768/161430005-8f8a4a6e-8955-4c70-959d-e53de563c6a1.jpg)