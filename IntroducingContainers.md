# Containers

- In any linux system
- in the root directory we have root , home,boot,sbin,bin,usr,var,dev,etc,opt,media
- these files have configuration ans all
- these are used by processes or sevices like apache , ngnix , mongodb etc
- they all are using the same bunch of files
- these processes do different different things but they are using teh same operating systems or the same directory structure
- so if we make any configurationto these files it will effect all the processes
- this the reason we need isolation
- so to isolate our services or processes
- we use different computers
- so to solve this issue we need more computers example apache will be a different computers and they have there own OS and more computer
- but the issue is more computers means more money
- here comes the concept of containers
- containers will be having its own file system its like an another operating system but its anctually not its like a miniature operating system
- so the Apache, Ngnix mongo they all will be different containers and having there own OS so now they all are independent
- will be having a virtualised network which will give IP addresses to all the containers for the inner communication
- so now our isolation problem is fixed
- these are very small and light weight and they dont have everything but only those which are needed to run that service
- so now we can archive them and these archives are known as Image
- the motto of creating an image is that we can ship it anywhere
- so this archive can be run in your local desktop and the same archive you can ship to the server and run that

# Docker

- Its an open platform for developing shiping and running applications
- it provides the ability to package and run an applicaiton in a loosely isolated enviroment called container
- the isolation and security allows you to run many containers simultaneosly on a given host
- `DOCKER HOST` is the docker service
- ``

# Hands on Docker Containers

- `system ctl status docker` to the the status of the docker
- `sudo docker run hello-world` docker run is to create a new container and hello world is called the image name (just for testing)
- `docker images` it will show you all the images that are present
- `docker ps` containers that are running
- `docker run --name web01 -d -p 9080:80 nginx` --name is to name a container web01 is an container name nginx is the image name in the docker hub , -d is for running this in the background not in the foreground, -p is for giving the port 9080 is the host port and 80 is the container port host is the VM , container will be running in the internally but to access it from outside we have to do port maping which is this -p 9080 : 80 so it routes the request from 9080 to port 80 of the container
- `docker inspect web01` here in place of the web01 its the container name there in the network inside the bridge you will see the IPAddress and thats the IP for the container
- `curl http://172.17.0.2:80` here the 172 part is the IP address and the 80 is the port for the container you will see html in this command
- `ip addr show` it will give you the IP for the VM example 192.168.29.249 this is the bridge IP
- `docker ps` to check the host port lets say 9080 now if you put the host IP:the port its gonna route the request to the container and it will return you the html
- `docker build -t testimg` this will be the image name and the location of the image
- `docker ps` to check all the containers take the port f the new container and put it in the browser along with the host machine IP
- `docker stop web01 relaxed_germain` to stop the containers give the containers names
- `docker rmi {all the image Ids}` fing all the images using docker images

# Vprofile project on containers

- Docker Compose is a tool for defining and running multi-container applications. It is the key to unlocking a streamlined and efficient development and deployment experience.
- `vagrant global -status --prune` to check the status of all the global virtual machines
- `vim docker-compose.yml` for creating a file for docker compose and the file name should be docker-compose.yml
- https://raw.githubusercontent.com/devopshydclub/vprofile-project/docker/compose/docker-compose.yml put this file content in the docker-compose file
- `docker compose up -d` its gonna download all the images run it where the compose file is there
- now check the ip using `ip addr show` and access the IP in the browser and it will open a website that is hosted in the container
- `docker compose down` it will stop all the containers and it will remove them
- `docker system prune -a` this command will remove all the stopped containers and the images that are not used

# Microservices

-
