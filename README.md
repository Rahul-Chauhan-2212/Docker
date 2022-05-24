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
<li>docker stop containerName  ---> To stop docker image/container</li>
</ul>
