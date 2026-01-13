Demo App – Developing with Docker

This demo app shows a simple user profile application set up using:

index.html with pure JavaScript and CSS styles

Node.js backend with Express module

MongoDB for data storage

All components are Docker-based.

With Docker
To start the application
Step 1: Create Docker network
docker network create mongo-network

Step 2: Start MongoDB
docker run -d -p 27017:27017 \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=password \
--name mongodb \
--net mongo-network \
mongo

Step 3: Start Mongo Express
docker run -d -p 8081:8081 \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
--net mongo-network \
--name mongo-express \
-e ME_CONFIG_MONGODB_SERVER=mongodb \
mongo-express


NOTE: Creating a docker network is optional.
You can start both containers in the default network.
In this case, just omit the --net flag in the docker run command.

Step 4: Open Mongo Express from browser
http://localhost:8081

Step 5: Create database and collection

Create database: user-account

Create collection: users
(using Mongo Express UI)

Step 6: Start Node.js application locally

Go to the app directory of the project:

npm install
node server.js

Step 7: Access Node.js application UI
http://localhost:3000

With Docker Compose
To start the application
Step 1: Start MongoDB and Mongo Express
docker-compose -f docker-compose.yaml up


You can access Mongo Express at:

http://localhost:8080

Step 2: Create database

Database name: my-db

Step 3: Create collection

Collection name: users
(using Mongo Express UI)

Step 4: Start Node.js server
npm install
node server.js

Step 5: Access Node.js application
http://localhost:3000

Build Docker Image from the Application
docker build -t my-app:1.0 .


The dot (.) at the end of the command denotes the location of the Dockerfile.
