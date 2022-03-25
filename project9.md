# STEP - 19
# PROJECT 9: Continous Integration Pipeline For Tooling Website

## INSTALL AND CONFIGURE JENKINS SERVER
## sTEP 1 - Install Jenkins server
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