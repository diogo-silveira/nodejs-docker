# Building and deploying Node apps on Docker.

This is a quicky step-by-step doco to get running with Docker and Node apps on Windows.
Firstly, open the link below, download and install Docker.( https://docs.docker.com/docker-for-windows/install/ ). *Node: In case your machine doesn't have Hyper-V enabled, please go your Windoes Settings "Turn Windows features on or off" and enable Hyper-V. It will require to restart your computer.

Second, create one account on Docker website to have access to multiple Docker containers to have you up and running with multiple Docker Images.( https://hub.docker.com/ )

Once you have installed Docker, open any CMD and enter:
docker --version
It should show something like 'Docker version 19.03.8, build afacb8b'.

Once you are done, you can enter your creadentions eather on the Docker App or with Docker CLI.
Using the Docker CLI, please enter:
docker login
-- enter username and password

Well done, you should be able to start working, but before lets be a little more familiar with Docker CLI. Please type:
 > docker --help
 
 We will be using a few of this commands, like:
 > docker image ls // list all built images
 > docker container ls // List all containers built
 > docker start {imagename} // start docker container 
 > docker stop {imagename} // stop docker container
 > docker build // this command needs more props to run, so keep it on mind, we'll see it below
 > docker run // this command needs more parameters to run, so keep it on mind, we'll see it below
 

Create a project and add the file Dockerfile with the configs in

Define a container with Dockfile 

// Use the official image as a parent image.
FROM node:current-slim

// Set the working directory.
WORKDIR /usr/src/app

// Copy the file from your host to your current location.
COPY package.json .

// Run the command inside your image filesystem.
RUN npm install

// Inform Docker that the container is listening on the specified port at runtime.
EXPOSE 8080

// Run the specified command within the container.
CMD [ "npm", "start" ]

// Copy the rest of your app's source code from your host to your image filesystem.
COPY . .


docker build --tag bulletinboard:1.0 .

docker run --publish 8000:8080 -d --name bb bulletinboard:1.0
