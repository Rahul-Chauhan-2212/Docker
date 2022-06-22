<i>
<h1>Docker</h1>

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

<h5>docker run -p 8080:80 -d imageId</h5>
-d is used to run the docker run cmd in detached mode.</br>

To attach to the already running detached container

<h5>docker attach imageId</h5>
or
<h5>docker logs -f imageId</h5>

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

<h5>docker image prune -a</h5>

### Automatically delete the stopped containers

<h5>docker run -p 3000:80 -d --rm imageId</h5>
Here --rm does this trick. One the containers is stopped it is automatically deleted

### Inspecting Images

<h5>docker image inspect imageId</h5>

### Copy Files to Running Container and vice-versa

<h5>docker cp test/ admiring_kalam:/test</h5>
<h5>docker cp admiring_kalam:/test .</h5>
<h5>docker cp admiring_kalam:/test/copy.txt .</h5>

### Naming and Tagging Images and Containers

Containers Naming</br>

<h5>docker run -d -p 80:80 --name containerName imageId</h5> 
--name name is used to give a name to container</br>
Images Naming and Tagging</br>
<h5>docker build -t repoName:tag .</h5>
Tag an image referenced by ID</br>
To tag a local image with ID “0e5574283393” into the “fedora” repository with “version1.0”:</br>
<h5>docker tag 0e5574283393 fedora/httpd:version1.0</h5>
Tag an image referenced by Name</br>
To tag a local image with name “httpd” into the “fedora” repository with “version1.0”:</br>
<h5>docker tag httpd fedora/httpd:version1.0</h5>
Note that since the tag name is not specified, the alias is created for an existing local version httpd:latest.</br>
Tag an image referenced by Name and Tag</br>
To tag a local image with name “httpd” and tag “test” into the “fedora” repository with “version1.0.test”:</br>
<h5>docker tag httpd:test fedora/httpd:version1.0.test</h5>

### Pushing Images to DockerHub

Create Docker repo in DockerHub</br>
rchauhan9102/node-app

<h5>docker tag oldname docker reponame</h5>
<h5>docker login</h5>
<h5>docker push reponame</h5>
<h5>docker logout</h5>

### Pulling Images from DockerHub

<h5>docker pull dockerimagename</h5>

## Managing Data and Working with Volumes

Image ---> READ ONLY Container ---> READ/WRITE

#### Different Kinds of Data

1)Application(Code+environment) --->Fixed(Stored in Image)</br>
2)Temprory App Data(i.e. entered user data) ---> Variable(Stored in Containers)</br>
3)Permanent App Data(i.e. User Accounts) ---> Must not be lost when containers restarts(Stored in Volumes)</br>

Project: data-volumes-starting-setup
This app creates file with title name and content of file will be feedback
docker build

### Type of External Data Storages

<ul>
<li>Volumes(Mananged By Docker)</li>
<li>Bind Mounts(Managed By You)</li>
</ul>

#### Volumes

Volumes are folders on your local machine which are mounted into containers.</br>

<h5>docker volume ls</h5>
1)Anonymous Volumes</br>
When container shuts down, anonymous volume will be deleted
</br>
</br>
2)Named Volumes</br>
When container shuts down, named volume is not deleted and data is persisted and once the container starts again the same data from that volume can be used.</br>
CMD to create named volume:</br>
<h5>docker run -d -p 3000:80 --rm --name feedback-app -v feedback:/app/feedback feedback-node:volume</h5>

To remove volumes:

<ul>
<li><h5>docker volume rm volumeName</h5></li>
<li><h5>docker volume prune</h5></li>
</ul>

### Bind Mounts

Used to persist editable data</br>
it is a volume inside your local machine which watches the changes inside the folder and copies it to container.

<h5>docker run -d -p 3000:80 --rm --name feedback-app -v feedback:/app/feedback -v "C:/Users/RAHUL CHAUHAN/Documents/Docker Codes/Docker/data-volumes-starting-setup:/app" -v /app/node_modules feedback-node:volume</h5>

##### Volumes Comparison

<table>
<tr>
<th>Anonymous Volume</th>
<th>Named Volume</th>
<th>Bind Mount</th>
</tr>
<tr>
<td>docker run -v /app/data</td>
<td>docker run -v data:/app/data</td>
<td>docker run -v path/to/code:/app/data</td>
</tr>
<tr>
<td>Created specifically for single container</td>
<td>Created in general-not tied to any container</td>
<td>Location on host file system, not tied to any specific container</td>
</tr>
<tr>
<td>Survives container shutdown/restarts until --rm is used</td>
<td>Survives container shutdown/re-start/removal via docker CLI</td>
<td>Survives container shutdown/re-start, removal on host file system</td>
</tr>
<tr>
<td>Can not be shared across containers</td>
<td>Can be shared across containers</td>
<td>Can be shared across containers</td>
</tr>
<tr>
<td>As it is anonymous. It can't be re-used even for same image.</td>
<td>Can be re-used for same container(across re-starts)</td>
<td>Can be re-used for same container(across re-starts)</td>
</tr>
</table>

###### Making Volumes Read-Only

By default all the volumes are read-write. Which means bind mounts can change our host machine code from the container which does not want. So for this <b>ro</b> is used in bind mounts

<h5>docker run -d -p 3000:80 --rm --name feedback-app -v feedback:/app/feedback -v "C:/Users/RAHUL CHAUHAN/Documents/Docker Codes/Docker/data-volumes-starting-setup:/app:ro" -v /app/temp -v /app/node_modules feedback-node:volume</h5>

###### Mananging Docker Volumes

<h5>docker volume ls</h5>
<h5>docker volume create volumeName</h5>
<h5>docker volume rm volumeName</h5>
<h5>docker volume prune</h5>
<h5>docker volume inspect volumeName</h5>

###### Ignoring files and folders while building images

<b>.dockerignore</b> file

#### ARGuments & ENVironment variables

Docker supports build-time ARGuments and run-time ENVironment variables

<ol>
<li>
<h4>ARG</h4>
Available inside of Dockerfile, not accessible in cmd or any application code</br>
Set on image build(docker build) via --build-arg</br>
<h5>docker build -t feedback-node:dev --build-arg DEFAULT_PORT=8000  .</h5>
</li>
<li>
<h4>ENV</h4>
Available inside of a Dockerfile and application code</br>
Set via ENV in Dockerfile or --env on docker run
<h5>docker run -d -p 3000:8000 --rm --name feedback-app --env PORT=8000 -v feedback:/app/feedback -v "C:/Users/RAHUL CHAUHAN/Documents/Docker Codes/Docker/data-volumes-starting-setup:/app:ro"  -v /app/node_modules -v /app/temp feedback-node:env</h5>
<h5>docker run -d -p 3000:8000 --rm --name feedback-app --env-file ./.env -v feedback:/app/feedback -v "C:/Users/RAHUL CHAUHAN/Documents/Docker Codes/Docker/data-volumes-starting-setup:/app"  -v /app/node_modules -v /app/temp feedback-node:env</h5> via .env file
</li>

</ol>

### Networking(Cross-) Container Communication

<ol>
<li><h5>Container and WWW communication</h5</br>
Container can communicate with WWW without any extra coding or configurationn.
</li>
<li><h5>Container and Local Host Machine Communication</h5></br>
for container and localhost communication, we need to change the server ip inside our docker images to host.docker.internal</br>
in local case : localhost  --> host.docker.internal
</li>
<li><h5>Container to container communication</h5></br>
There can be two approaches:</br>
<ul>
<li>Basic Solution</br>
Look for the ip address of the container to be used using <b>docker container inspect containername</b></br>
then use this ip in the image of the main app.
</li>
</ul>
</li>
</ol>
<span>app used: <b>networks-starting-setup</b></span>

</i>
