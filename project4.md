
# PROJECT 4 - MEAN STACK DEPLOYMENT TO UBUNTU IN AWS

## Step 0
Configuring ec2-instance and connecting via aws-CLI console
![cli1](https://user-images.githubusercontent.com/34573768/158013022-c2699cd1-1b28-4bb9-a2d8-ea678c3b2d31.png)

## Step 1: Install NodeJs
The following steps update and upgrade Ubuntu on aws-cli

`sudo apt update`

`sudo apt upgrade`

The following commands added certificate to the configuration

`sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates`

`curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -`

`sudo apt install -y nodejs`

## Step 2: Install MongoDB

`sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6`

`echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list`

This command installed MongoDB

`sudo apt install -y mongodb`

This command Started The server

`sudo service mongodb start`

Verify that the service is up and running

`sudo systemctl status mongodb`

![server1](https://user-images.githubusercontent.com/34573768/158013548-980930b7-49c2-4eb9-bf60-7b1669ebbec2.png)

Install npm – Node package manager

`sudo apt install -y npm` (It failed to download and returned error message in the console
![npm1](https://user-images.githubusercontent.com/34573768/158013770-95ab4a94-1373-462a-a4c9-be4cfc29ea65.png)

NB: Frome the answers i discovered online, installing `sudo apt install -y nodejs` automatically installed `npm` package. and i ran npm -v indicated that npm version 6.14.16 is present.
![npm2](https://user-images.githubusercontent.com/34573768/158014367-4cdc2c15-b015-47f0-931c-08819011a72b.png)

Install body-parser package (We need ‘body-parser’ package to help us process JSON files passed in requests to the server)

`sudo npm install body-parser`

Create a folder named ‘Books’ and change directory into the folder

`mkdir Books && cd Books`

Adding files and packages into the directory
`npm init`

Added `server.js` file to the book directory

`touch server.js`

`vi server.js`

![server2](https://user-images.githubusercontent.com/34573768/158014852-31ede200-0eda-4a6b-a802-96d8b427ac94.png)


## Step 3: INSTALL EXPRESS AND SET UP ROUTES TO THE SERVER

Express Mongoose installed in the Books folder

`sudo npm install express mongoose`

In ‘Books’ folder, create a folder named apps

`kdir apps && cd apps`

Create a file named routes.js

`touch routes.js`

Edit routes.js file

`vi routes.js`

![routes](https://user-images.githubusercontent.com/34573768/158015337-54119dec-5951-4486-9216-b8b41aee4acf.png)

Create Models folder in the Apps directory and change into it

`mkdir models && cd models`

Create books.js file in the Models folder

`touch books.js`

`vi books.js`

![books](https://user-images.githubusercontent.com/34573768/158015297-566442a7-b4f8-4ae8-ad11-773875f315a3.png)


## Step 4 – ACCESS THE ROUTES WITH ANGULARJS

Change back to Books directory

`cd ../..`

`mkdir public && cd public`

Create script.js file and add config to it

`touch script.js`

`vi script.js`
![script](https://user-images.githubusercontent.com/34573768/158015797-64c57a9f-86b6-470a-819c-5650594d1c19.png)

Create index.html file

`touch index.html`

`vi index.html`

![index](https://user-images.githubusercontent.com/34573768/158015910-96a07b8f-1595-4a01-971c-5e39ca5fab91.png)

Start server

`node server.js` It threw error (I realised that a .js file is added wrongly. it expected `book.js` but i added `books.js`. I corrected it and it works
![server3](https://user-images.githubusercontent.com/34573768/158016241-619b132c-804f-4462-8326-eddc043a2c48.png)

`curl -s http://localhost:3300`
![server4](https://user-images.githubusercontent.com/34573768/158016705-9b534f93-96d1-4cc9-9e30-a5c7a9f0cc86.png)

My webpage display info

`http://3.16.163.249:3300/`

![web1](https://user-images.githubusercontent.com/34573768/158016902-044fab26-5788-4738-a8ec-63bb0af15667.png)

![web2](https://user-images.githubusercontent.com/34573768/158017638-48ef0fe3-b2b7-426a-ac6e-915bd72a64b4.png)

## Completed


# Learning discovery

Project 4 has less direction commands as some actions were purposely left out but with the following commands giving clue of what has been left out. I quite like as it prompt me to remember what to use and how to use it, maybe it was because it was not opaque to remember.
I have made up my mind not to use project video just to see how i was going to cope but i was disappointed that i had to use project-4 video on three occassions;
1. When i created `server.js` file and i saved it, i was expecting IDE to return to normal display but it didn't so i had to check with the project-4 video to see how it was done.
2. When i started the server using node `node server.js`, it threw and error and i couldn't figure it out after staring at it for a while. I did saw a bold message `Module /Books/models/book ` not found but it did not click that i have used books.js instead. so i checked the video and exact same mistake was mentioned so i corrected it and it works.
3. I check the video to find out how to work out `curl -s http://localhost:3300`.

Overall, i'm glad they made the video and it serve a good purpose.





