# STEP 11 
# Aux Project 1 (Shell Scripting)

## AUX PROJECT 1: SHELL SCRIPTING

cd to .pem dir `cd Downloads`

connect to the instance

change connection to root user `sudo su`

create directory `mkdir Shell`

create shell script `vi onboard.sh`

move shell script into Shell directory `mv onboard.sh Shell/`

move into the dir - `cd Shell`

check the item in the dir `ls` = Onboard.sh

change to write modification `chmod +x onboard.sh`
 
add user names ` vi names.csv`
 
generate pub and priv key `ssh-keygen` (follow the instruction)

check - `ls -l /root/.ssh`
 
edit & update shell script `vi onboard.sh` add /root/.ssh/
 
change dir to ssh `cd /root/.ssh/`

check working dir `pwd` (/root/.ssh/)

change dir `cd, ls - snap, cd, ls-ubuntu`

change dir to `cd ubuntu/Shell/` 

check dir `ls` (names.csv, onboard.sh)

create developers group `groupadd developers`
 
run shell script `./onboard.sh (created successfully)
![dev1](https://user-images.githubusercontent.com/34573768/158427072-f325c900-632a-4bf1-912f-f3cfb5efbafe.png)
 
check for users details `ls -l /home/` (reveals user names)
![dev2](https://user-images.githubusercontent.com/34573768/158427174-b0328542-7737-4534-b7ed-f6949790a2f9.png)
 
connect as one of the user `ssh + userName@publicIp` (it should connect successfully)
![dev3](https://user-images.githubusercontent.com/34573768/158427336-41ee9aaf-8e44-4903-833c-c8d9f8bfebbb.png)
