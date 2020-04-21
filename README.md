# Building and deploying Node apps on Docker.

##### This is a quick step-by-step to get running with Docker and Node apps on Windows.

> Firstly, open the link, download and install Docker. --> ( https://docs.docker.com/docker-for-windows/install/ ). 
> `Note:` In case your machine doesn't have Hyper-V enabled, please go your Windows Settings "Turn Windows features on or off" and enable Hyper-V. It will require to restart your computer.

> Second, create one account on Docker website to have access to multiple Docker containers to have you up and running with multiple Docker Images.( https://hub.docker.com/ )

> Once you have installed Docker, open any CMD and enter:
```
docker --version

> It should show something like 'Docker version 19.03.8, build afacb8b'.
```
> Congrats, you have Docker up and running.

> Now, you can enter your credentials either on the Docker App or with Docker CLI.
> Using the Docker CLI, please enter:
```
docker login
>
> enter username and password
```
Well done, you should be able to start working, but before let's get a little more familiar with Docker CLI. Please type:
 ```
 docker --help
``` 
 We will be using a few of these commands, like:
 > docker image ls // list all built images
 > docker container ls // list all containers built
 > docker start {imagename} // start docker container 
 > docker stop {imagename} // stop docker container
 > docker build // this command needs more props to run, so keep it on the mind and we'll see it below
 > docker run // this command needs more props to run, so keep it on the mind and we'll see it below
 
 Please, visit this link ( https://docs.docker.com/engine/reference/commandline/docker/ ) to get known all commands.

> In this example I am going to be using a docker project from Git called bulletinboard, this is available on git for clone on ( https://github.com/dockersamples/node-bulletin-board )

> Clone this repository to your local
```
git clone https://github.com/dockersamples/node-bulletin-board.git
```
> Please, open this project with your preferred IDE and take a look at the file `Dockerfile`.

This project has the Dockerfile with the configurations needed in order to run the app inside a docker.

```
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
```

> So, we learned that in case you need to create a new app and deploy inside docker, you require this file to trigger some configurations on the deploy.

### Next steps
> Let's now build our image. Using your CMD navigate to the file directory where you have the file 'Dockerfile'. 
> And run the command below:
```
docker build --tag bulletinboard:1.0 .

> It should execute the file 'Dockerfile' with all specific commands, build the image and target the name bulletinboard with the  version 1.0

```
> Cool, now let's check if the image has succeeded built. Just type:
```
docker image ls

> And it should print a list of images available
```
> But it's important to note, it's only the image, we still have to deploy this image inside the container, so, let's check before if we have an existing container. Let's type:
```
docker container ls --aa

> It should display the number of containers you have built with some additional information.
```

> Nice, so now we can deploy a container. Let's do it by running:
```
docker run --publish 8000:8080 --detach --name bb bulletinboard:1.0
> It will deploy our image inside a container, forwarding all traffic from localhost:8080 to 8000, keeping it running by the command `detach`, and, with a new name `bb` and using exactly the same image and version bulletinboard:1.0 
```
> Now, let's check again our list of containers by running:
```
docker container ls --aa
```
> Cool, if everything went through correctly, you should get a built container running with a docker image forwarding any incoming requests from localhost:8080 to localhost:8000, so let's open your browser and enter:
```
http://localhost:8000
```

> Nice, you have created your first Docker. Now you can play with lots more options and images with Docker.

Thanks for following up until the end of this exercise.
