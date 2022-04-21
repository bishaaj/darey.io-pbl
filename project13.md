# STEP 23
# ANSIBLE DYNAMIC ASSIGNMENTS (INCLUDE) AND COMMUNITY ROLES

Project 13 is about how DevOps engineer can configure Ansible-playbooks to execute a static or Dynamic job flows with the use of 'import and include'

## Introducing Dynamic Assignment Into Our structure
I started by creating a new branch called 'dynamic-aasignment' on the ansible-config-mgt repo and i added a yml file to it 'env-vars.yml'

![image](https://user-images.githubusercontent.com/34573768/164487910-cf00c6c4-7f73-4e38-9bc1-0e78d6b74bd0.png)

My env-vars.yml file look like the image below 
![image](https://user-images.githubusercontent.com/34573768/164488219-ace08cf0-4b98-4a1e-8188-b878bc6e18dc.png)

While i updated the playbook/site.yml file to image below
![image](https://user-images.githubusercontent.com/34573768/164488415-f992b019-b44b-48ad-89a1-fbe85df47a21.png)

## Community Roles
I added a community role to the configuration by downloading Mysql Ansible Role using 'geerlingguy'
`cd roles`
`ansible-galaxy install geerlingguy.mysql`
`mv geerlingguy.mysql/ mysql`

After the above, i edited the `roles/mysql/default/main.yml/` path to mirror my database set up
I repeated the above steps for Apache and nginx load balancers

## Step 3: Load Balancer roles
You could create your own roles for both nginx and apache (or grab mine from https://github.com/bishaaj/ansible-config-mgt/tree/master/roles)
Since you cannot use both Nginx and Apache load balancer, you need to add a condition to enable either one - this is where you can make use of variables.

Declare a variable in defaults/main.yml file inside the Nginx and Apache roles. Name each variables enable_nginx_lb and enable_apache_lb respectively.

Set both values to false like this enable_nginx_lb: false and enable_apache_lb: false.

Declare another variable in both roles load_balancer_is_required and set its value to false as well

Update both assignment and site.yml files respectively

loadbalancers.yml file
![image](https://user-images.githubusercontent.com/34573768/164490951-8f616037-5b18-40b0-ad70-fe213fb2d3d5.png)
![playbook1](https://user-images.githubusercontent.com/34573768/164491171-7dccf035-8749-43c0-8ee6-5d0fadd7e816.jpg)
![playbook2](https://user-images.githubusercontent.com/34573768/164491186-24d68b78-0234-4654-b712-19f1ace5c445.jpg)
![playbook3](https://user-images.githubusercontent.com/34573768/164491201-c204f5ca-dcde-45a8-818f-8b182397ae12.jpg)
![playbook4](https://user-images.githubusercontent.com/34573768/164491212-95995200-d809-4f3c-b012-ffb25e13b48c.jpg)
![playbook5](https://user-images.githubusercontent.com/34573768/164491398-6d8ff581-9f82-4fdf-a826-401cbc6c89b7.jpg)
![playbook7](https://user-images.githubusercontent.com/34573768/164491414-59394ac9-2074-44e6-9fc5-a3cd3e6c4280.jpg)