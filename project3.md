# STEP 5

## Project 3 - MERN STACK IMPLEMENTATION

## Introduction
MERN stack is another combination of open source tools within web application and software management. MERN uses combination of database, espress js, react and node js. this make it one of the most sought after stack as it enables building faster and reliable web applications and offer end to end development.

## Step 1 – BACKEND CONFIGURATION

`sudo apt update`

`sudo apt upgrade`

`curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -`
![node1](https://user-images.githubusercontent.com/34573768/157474699-b71a3504-c678-44d2-8a32-a224d245bbbe.png)

`sudo apt-get install -y nodejs`

`node -v` Verifying node version

![node2](https://user-images.githubusercontent.com/34573768/157474789-7dc3d309-f5db-49fc-9777-9d6856c5c1c7.png)

`npm -v` Verifying npm version

![node3](https://user-images.githubusercontent.com/34573768/157474899-31576be2-a533-4c1d-ba77-dac20165b27c.png)

`mkdir Todo` Created a Todo folder

![dir1](https://user-images.githubusercontent.com/34573768/157475022-ff5bb076-1043-4d6a-8c9d-6debc981d02f.png)

`npm init` Downloads package.json in the directory

![npm1](https://user-images.githubusercontent.com/34573768/157475219-b93ad8d9-f7a9-4099-8ee0-abfb6758ef8b.png)

`ls` List to check all directories and files

![ls1](https://user-images.githubusercontent.com/34573768/157475483-7b493ba7-4256-418a-b277-bb2c8ba14d95.png)


## INSTALL EXPRESSJS

`npm install express`

`touch index.js` created index.js file

![ls2](https://user-images.githubusercontent.com/34573768/157475693-dba0b82f-9089-4830-8b7a-cbb165033bfa.png)

`npm install dotenv`

`node index.js`

![node4](https://user-images.githubusercontent.com/34573768/157475786-7349a09c-5b2d-452c-a7b6-025e055e417a.png)

`http://18.216.200.244:5000/` public ipaddress page

![host1](https://user-images.githubusercontent.com/34573768/157475898-0318cada-61a0-422e-b735-e1355e8e13a7.png)

`mkdir routes`

`cd routes`

![dir2](https://user-images.githubusercontent.com/34573768/157476116-cc870170-0679-43f1-a89d-88cfaeb8b810.png)

`touch api.js`

`vim api.js`

## MODELS

`npm install mongoose`

`mkdir models`

`cd models`

`touch todo.js`

## MONGODB DATABASE

- [Shared cluster account](https://cloud.mongodb.com/v2/6226fef52df552008e93bbe5#clusters)

`cat .env` To reveal .env file details

![env1](https://user-images.githubusercontent.com/34573768/157476282-46c0266f-1335-43ba-b9ef-8420c63e2732.png)

`node index.js`

![db1](https://user-images.githubusercontent.com/34573768/157476500-3c782310-6529-4809-b016-92f8a9fe4f46.png)

`http://18.216.200.244:5000/api/todos`

![api1](https://user-images.githubusercontent.com/34573768/157476567-2df36f2e-1766-45dd-87f1-1a54594d8e79.png)

`Get: todo list`

![api2](https://user-images.githubusercontent.com/34573768/157476639-60d2eab5-75e3-4e52-8d1f-351b39fb7bb2.png)


## Step 2 - FRONTEND CREATION

` npx create-react-app client`

`npm install concurrently --save-dev`

`npm install nodemon --save-dev`

`vi package.json`

`npm run dev`

![npm2](https://user-images.githubusercontent.com/34573768/157476754-1811cbbe-6cbd-4c62-999d-41b549b594da.png)

`cd src`

`mkdir components`

`cd components`

`touch Input.js ListTodo.js Todo.js`

![ls3](https://user-images.githubusercontent.com/34573768/157476837-3da3ba57-7c26-4261-900f-77a9dd067b2d.png)

`vi Input.js`

`npm install axios`

## FRONTEND CREATION (CONTINUED)

`cd src/components`

`vi ListTodo.js`

`vim index.css`

`npm run dev`
- [my public ipaddress](http://3.144.132.172:3000/)

![todosList](https://user-images.githubusercontent.com/34573768/157476964-613d7fc2-af85-4e46-9962-cea74ab25467.png)
