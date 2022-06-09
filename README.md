# Docker

### Docker is a container management service. The keywords of Docker are develop, ship and run anywhere. The whole idea of Docker is for developers to easily develop applications, ship them into containers which can then be deployed anywhere.

#### Features of Docker

<ul>
<li>Docker has the ability to reduce the size of development by providing a smaller footprint of the operating system via containers.</li>
<li>With containers, it becomes easier for teams across different units, such as development, QA and Operations to work seamlessly across applications.</li>
<li>You can deploy Docker containers anywhere, on any physical and virtual machines and even on the cloud.</li>
<li>Since Docker containers are pretty lightweight, they are very easily scalable.</li>
</ul>

#### Components of Docker

<ul>
<li><b>Docker Desktop</b> − It allows one to run Docker containers on the Windows/Mac OS.</li>
<li><b>Docker Engine</b> − It is used for building Docker images and creating Docker containers.</li>
<li><b>Docker Hub</b> − This is the registry which is used to host various Docker images.</li>
<li><b>Docker Compose</b> − This is used to define applications using multiple Docker containers.</li>
</ul>

#### Install Docker Desktop on Windows

Download Docker from link https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe

Note: When prompted, ensure the Use WSL 2 instead of Hyper-V option on the Configuration page is selected or not depending on your choice of backend.

If your admin account is different to your user account, you must add the user to the docker-users group. Run Computer Management as an administrator and navigate to Local Users and Groups > Groups > docker-users. Right-click to add the user to the group. Log out and log back in for the changes to take effect.

#### Some Initial Useful Docker Commands

<ul>
<li>docker --version ---> To get the docker version installed</li>
<li>docker build .   ---> To build docker image of the app</li>
<li>docker run -p portId:portId imageId ---> To run docker image on the given port</li>
<li>docker ps  ---> To list down the docker images running </li>
<li>docker ps -a  ---> to list down all the docker instances stopped or running</li>
<li>docker stop containerName  ---> To stop docker image/container</li>
</ul>

### Images vs Containers

Containers--> The running "unit of software" / running instance of Image
Multiple containers can be created based on one image
Images--> Templates of containers / contains code and required tools and runtime environment

##### Pre-Built Images

Docker Hub
example: node image at docker hub
cmd---> docker run -it node </br>

<h4>-it</h4> <span>to open node interractive shell</span></br>
Snippet--> </br>
Digest: sha256:52bda4c171f379c1dcba5411d18ed83ae6e99c3751cad67a450684efb9491f6b
Status: Downloaded newer image for node:latest

### Custom Images

Node JS App

<h4>Docker File :</h4>

<ul>
<li>FROM node ---> base image instruction</li>
<li>WORKDIR /app --->working directory in image</li>
<li>COPY . /app ---> copy all code file to working dir</li>
<li>RUN npm install ---> command to install node dependencies in image</li>
<li>CMD [ "node", "server.js" ] ---> command to run app in container not in image</li>
</ul>
Commands to build and run node js app image/container
<ul>
<li>docker build .</li>
<li>docker run -p 80:80 imageId</li>
</ul>

#### Image Layers

Each Command in Docker File creates a cacheable image layers. So we should be very specific to run commands in manner which have changes from very frequent to less frequent. So that the caching can be used properly and decrease the image build time.

### Stopping and Restarting Containers

docker run imageId --->creates and run new container
docker stop imageName ---> stop docker container
docker start imageName ---> run stopped container

### Attached and Detached Containers

docker run cmd run in attached mode which means the command prompt will be attached with the container which will show any console log on the same terminal.
docker start cmd run in detached mode.

<i>docker run -p 8080:80 -d imageId</i>
-d is used to run the docker run cmd in detached mode.</br>

To attach to the already running detached container
<i>docker attach imageId<i>
or
<i>docker logs -f imageId</i>

### Entering Interactive Mode

example: python-app-docker </br>
docker run imageId command Fails here</br>

<h5>docker run -it imageId</h5>

docker start -a containerId this command also not works correctly

<h5>docker start -a -i containerId</h5>
so -i serves as run containers in interactive mode

#### Deleting Images and containers

<h5>docker rm containerId</h5> 
Note: Container should be in stopped mode for this command</br>
To List down docker images
<h5>docker images<h5>

To delete Docker images

<h5>docker rmi imageId</h5>
Note:Only that image can be deleted which is not attached to any running or stopped container.So first have to delete containers then image.</br>

To Delete all the unused Docker Images

<h5>docker images prune</h5>
