#### CONNECT TO EC2 INSTANCE
``` ssh -i "key-pair-2.pem" ec2-user@ec2-15-206-89-115.ap-south-1.compute.amazonaws.com ```

#### INSTALLATION GUIDE: https://www.cyberciti.biz/faq/how-to-install-docker-on-amazon-linux-2/

#### For amazon linux: 
```
$ sudo yum install docker
$ sudo systemctl start docker.service
```
```
For ubuntu: sudo apt install docker.io
```
```
usermod -aG docker ubuntu
```
```
sudo apt-get install docker-compose
```

#### MOST USED COMMANDS - shell script (vi script.sh)
```
#!/bin/bash
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
docker rmi $(docker images -q) -f
docker system prune -y
git pull origin master
docker-compose up
```

#### nginx server
```
docker run -d --name c1 -p 80:80 nginx
```

Expose local-machine-port:internal-container-port. In this case, you are mapping port :80 in the container to port :80 on the server.
nginx is the name of the image on Docker Hub.

#### DOCKER IMAGE

#### RUN AN IMAGE
```
docker run --name c001 -p 4200:4200 image-1 /bin/bash // create container and get inside it
docker run -d --name c001 -p 3000:3000 image-1 // without volume
docker run -d -p 3000:3000 --name c001 -v volume-1 image-1 // with volume
docker inspect c001
```

#### CURL TO TEST IMAGE
```
ifconfig // copy docker0 inet address (172.17.0.1)
curl 172.17.0.1:3000
```

#### LIST ALL IMAGES
```
docker image ls
```

#### LIST TOP 5 IMAGES
```
docker images | head -5
```

#### LIST DOCKER IMAGES STORED LOCALLY
```
docker images
```

#### REMOVE AN IMAGE
```
docker image rm image_name
```

#### REMOVE ALL IMAGES
```
docker rmi $(docker images -a -q)
```

#### BUILD IMAGE
```
docker build docker_file_path OR
docker build -t image-1 .
```

#### TAG AN IMAGE
```
docker tag image_id tag_name
```

#### PRINT IMAGE HISTORY
```
docker history image
```

#### LOW LEVEL INFORMATION ABOUT IMAGE
```
docker inspect image
```

#### DELETE AN IMAGE FROM LOCAL STORAGE
```
docker rmi image_id
```

#### CREATE NEW IMAGE OF AN EDITED CONTAINER
```
docker commit container_id user_name/image_name
```
#### PULL IMAGE FROM DOCKER HUB (hub.docker.com) 
```
docker pull image_name
```

#### RUN IMAGE WITH MOUNT
```
docker volume create myVolume
docker run -d -p 3000:3000 --name c001 image_name --mount source=myVolume
// to see the volume inside container
docker inspect container_id  // find the mounts: [{ object 
```
#### DOCKER CONTAINER

#### LOGIN INTO CONTAINER:- INSIDE THE CONTAINER - RUN COMMANDS TO INSTALL SOMTHING INSIDE 
```
docker run -d --name c001 image_name
docker exec -it c001 /bin/bash
apt-update
apt-get install package name
```

#### INSPECT A CONTAINER ( entire details of a container )
```
docker inspect container_name 
```

#### LIST RUNNING CONTAINERS
```
docker ps
```

#### LIST RUNNING/ EXITED CONTAINERS
```
docker ps -a
```

#### STOP ALL CONTAINERS
```
docker stop $(docker ps -q)
```

#### LIST EXITED CONTAINER
```
docker ps -a -f status=exited   // ( -f: filter by )
```

#### REMOVE A CONTAINER
```
docker rm container_id
```

#### STOP ALL CONTAINERS AND REMOVE ALL CONTAINERS
```
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```

#### REMOVE ALL EXITED CONTAINERS
```
docker rm $(docker ps -a -f status=exited -q)    // (-q: pass the IDS to docker rm command)
```

#### LIST ALL EXITED OR CREATED CONTAINERS
```
docker ps -a -f status=exited -f status=created
```
#### REMOVE ALL EXITED OR CREATED CONTAINERS
```
docker rm $(docker ps -a -f status=exited -f status=created -q)
```
#### RUN AND REMOVE - REMOVE A CONTAINER UPON EXITING
```
docker run --rm
```
#### CREATE CONTAINER FROM AN IMAGE
```
docker run -it -d image_name
```
#### CREATE A NEW CONTAINER FROM AN IMAGE
```
docker create image
```
#### START CONTAINER
```
docker start container
```
#### STOP CONTAINER (GRACE FULLY)
```
docker stop container_id
```
#### STOP CONTAINER (FORCE FULLY)
```
docker kill container_id
```
#### PAUSE CONTAINER
```
docker pause container
```
#### UNPAUSE CONTAINER
```
docker unpause container
```
#### RESTART CONTAINER
```
docker restart container
```
#### DOCKER EXEC | ACCESS THE RUNNING CONTAINER
```
docker exec -it container_id bash
```
#### DELETE STOPPED CONTAINER
```
docker rm container_id
```
#### WAIT CONTAINER/ BLOCK CONTAINER
```
docker wait container
```
#### CREATE A NEW IMAGE FROM A CONTAINER
```
docker commit container image 
```
#### DOCKER EXPORT CONTAINER:- Exports container contents to a tar archive
```
docker export container
```
#### DOCKER ATTACH CONTAINER:- Attaches to a running container
```
docker attach container
```
#### SAVE A RUNNING CONTAINER AS AN IMAGE
```
docker commit -m "commit message" -a "author" container user_name/image_name:tag
```
#### CONTAINER LOGS
```
docker logs -ft container
```
#### RUN A COMMAND IN A CONTAINER
```
docker exec -it container script.sh
```
#### REMOVE A CONTAINER AND IT'S VOLUME
```
docker rm -v container_name
```
#### DOCKER VOLUME
#### CREATE VOLUME
```
docker volume create volume-1
```
#### LIST ALL VOLUMES
```
docker volume ls
```
#### REMOVE A VOLUME
```
docker volume rm volume-1
```
#### REMOVE ALL VOLUMES
```
docker volume prune
```
#### REMOVE MULTIPLE VOLUMES
```
docker volume rm volume-1 volume-2
```
#### INSPECT VOLUME
```
docker volume inspect volume-1
```

#### MOUNT A VOLUME ON CONTAINER
```
docker run -d -p 3000:3000 --name c001 image_name --mount source=myVolume
```
#### DOCKER REPOSITORY 
// ( SERVICE: AMAZON ELASTIC CONTAINER REGISTRY | PUSH IMAGE TO REPO. )

#### INSTALL AWS CLI (Optional)
```
> sudo apt install awscli
```
#### CREATE YOUR ACCESS KEY FROM BELOW LINK (Optional)
```
https://us-east-1.console.aws.amazon.com/iamv2/home####/security_credentials
``````

#### CONFIGURE AWS (Optional)
```
> aws configure
-> access id
-> accesss password
-> region (us-east-1) // region matters, the repository will be created in this region only.
```

#### IF WANNA CLEAN YOUR DOCKER (optional)
```
docker system prune
```
#### REMOVE ALL IMAGES (optional)
```
docker rmi $(docker images -q) -f
```
#### CREATE A NEW REPOSITORY 
```
IMPORTANT:- repository name and image tag name should be same ( example:- my-app )
https://us-east-1.console.aws.amazon.com/ecr/repositories
```
#### GO TO CONSOLE
```
#### AUTHENTICATE YOUR AWS ACCESS ID AND PASSWORD
``````
> aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 522574855415.dkr.ecr.us-east-1.amazonaws.com
```

#### BUILD IMAGE
```
docker build -t my-app .
```
#### TAG THE IMAGE TO PUSH
```
docker tag my-app:latest 522574855415.dkr.ecr.us-east-1.amazonaws.com/my-app:latest
```

#### PUSH THE IMAGE TO REPOSITORY
```
docker push 522574855415.dkr.ecr.us-east-1.amazonaws.com/my-app:latest
```
#### SELECT THE REGION (us-east-1)
```
#### CHECK YOUR AWS REPOSITORY IN given region (us-east-1)
```
-> CLICK ON repo my-app
-> You should find the image pushed.
```
#### DOCKER SERVICE

#### CONTROL DOCKER SERVICES
```
sudo systemctl start docker.service 
sudo systemctl stop docker.service 
sudo systemctl restart docker.service
sudo systemctl status docker.service 
````
#### FLAGS RUN COMMANDS - (CREATE CONTAINER FROM IMAGE) 

#### SYNTAX: docker run (options) image (command) (arg...)

#### RUN A CONTAINER IN THE BACKGROUND AND PRINT THE CONTAINER ID
```
--detach, -d
```
#### SET ENVIRONMENT VARIABLES
```
--env, -e
```
#### SET A HOSTNAME TO A CONTAINER
```
--hostname, -h
```
#### CREATES A META DATA LABEL FOR A CONTAINER
```
--label, -l
```
#### ASSIGN A NAME TO A CONTAINER
```
--name
```
#### CONNECT A CONTAINER TO A NETWORK
```
--network
```
#### REMOVE CONTAINER WHEN STOPS
```
--rm
```
#### SET READ ONLY FILE SYSTEM FOR A CONTAINER
```
--read-only
```
#### SET A WORKING DIRECTORY IN A CONTAINER
```
--workdir, -w
```

--------------------------------------------------------------------------------------------- DOCKER SYSTEM 

#### CLEAN DOCKER - remove all images, containers, volumes and networks- 
```
that are untagged or stopped.
docker system prune
```
#### DOCKER INSTALLATION/ INFO/ START DOCKER SERVICE

#### INSTALL DOCKER
```
sudo yum install docker
```
#### START DOCKER
```
sudo service docker start
sudo systemctl enable docker.service
```

#### CHECK DOCKER INFORMATION
#### docker info
#### DOCKER VERSION
```
docker --version
```
#### CHECK DOCKER SERVICE STATUS
```
sudo systemctl status docker.service
```
--------------------------------------------------------------------------------------------- DOCKER SERVICE

#### CONTROL DOCKER SERVICES
```
sudo systemctl start docker.service 
sudo systemctl stop docker.service 
sudo systemctl restart docker.service
sudo systemctl status docker.service 
```
#### LIST ALL SERVICES RUNNING IN SWARM
```
docker service ls
```
#### LIST ALL RUNNING SERVICES
```
docker stack services stack_name
```
#### CREATE NEW SERVICE
```
docker service create image
```
#### UPDATE A SERVICE
```
docker service update service_name
```
#### LIST TASKS OF A SERVICE
```
docker service ps service_name
```
#### SCALES ONE OR MORE REPLICATED SERVICE
```
docker service scale service_name=10
```
#### LIST ALL SERVICE LOGS
```
docker service logs stack_name service_name
```
#### DOCKER HUB ( REGISTRY )

#### LOGIN TO DOCKER HUB OR REGISTRY
```
docker login
```
#### LOGOUT FROM REGISTRY
```
docker logout
```
#### PULL IMAGE FROM REGISTRY
```
docker pull mysql
```
#### PUSH IMAGE TO REGISTRY
```
docker push repo/ rhel-httpd:latest
```
#### SEARCH IMAGE IN DOCKER HUB
```
docker search image_name
```
#### DOCKER PUSH:- Push an image to the docker hub repository
```
docker push user_name/image_name
```

#### DOCKER NETWORK AND NETWORK ISOLATION

#### CREATE A NEW NETWORK
```
docker network create secure-network
```
#### DETAIL INFORMATION OF A NETWORK
```
docker network inspect secure-network OR 
docker inspect secure-network
```
#### REMOVE A NETWORK
```
docker network rm network_name
```
#### LIST ALL NETWORKS
```
docker network ls
```
#### CONNECT A CONTAINER TO A NETWORK
```
docker network connect secure-network login-container
```
#### DISCONNECT A CONTAINER FROM A NETWORK
```
docker network disconnect secure-network login-container
```

EXAMPLE:-
#### Create 2 containers (login, logout) with nginx image
```
docker run -d --name login nginx:latest
```
#### Get inside login container, update apt, install ping command
```
docker exec -it login /bin/bash
apt update
apt-get install iputils-ping -y
```
#### check version of ping
```
ping -v
```
#### Create logout container
```
docker run -d --name logout nginx:latest
```
#### check ip address of both containers
```
docker inspect login // 172.17.0.2
docker inspect logout // 172.17.0.3
```
Both container is in same network, because we are using default bridge network (veth0 || docker0 || bridge network. Both containers can ping each other

#### log into (get inside) Login container and ping the Logout container
```
docker exec -it login /bin/bash
ping 172.17.0.3
```

#### Both are pinging to each other, because they are using default bridge network, which allows containers to talk to each other.

#### WHAT IS THE TYPE OF NETWORK THEY ARE USING ?
```
docker inspect login
```
#### You will find the network inside bridge object.
#### LIST ALL NETWORKS
```
docker network ls
```
#### CREATE A TEST NETWORK AND DELETE IT
```
docker network create test
docker network ls
docker network rm test
```
#### CREATE A CONTAINER `FINANCE` WITH NETWORK ISOLATION (CUSTOM BRIDGE NETWORK)
```

###```# CREATE A CUSTOM BRIDGE NETWORK named secure-network
```
docker network create secure-network
```
#### ASSIGN SECURE NETWORK TO FINANCE CONTAINER, SEE IF LOGIN CONTAINER CAN TALK TO FINANCE CONTAINER
```
-> No other container should connect connect to secure network (custom bridge n/w) or talk to containers connected to secure network as these container have sen```sitive information.

#### CREATE FINANCE CONTAINER AND CONNECT IT TO SECURE NETWORK
```
docker run -d --name finance --network=secure-network nginx:latest
```
#### INSPECT FINANCE CONTAINER AND CHECK WHICH NETWORK IS IT CONNECTED TO ?
```
-> should be connected to secure network with different IP Address subnet ID.
docker inspect finance
-> network should 'secure-network'
```
#### LOG INTO LOGIN CONTAINER AND TRY PINGING FINANCE CONTAINER
```
docker exec -it login /bin/bash
ping ip_address_of_finance_container

// should not be able to ping.
```
#### RUN AN IMAGE WITH CONNECTED TO secure-network NETWORK
```
docker run -d --name host-nw-container --network=secure-network nginx:latest
```
#### START AN EXISTING CONTAINER CONNECTED TO SPECIFIC NETWORK
```
docker start --network=secure-network login-container
docker ps
docker inspect host-nw-container
-> you will see networking is host.
-> no ip address is assigned to this container.
-> docker didn't create any virtual network for this container because container is connected to host network, so it can be directly accessed with host ip address. container virtual ip address isn't required.
```

#### DISCONNECT A CONTAINER FROM bridge network AND CONNECT IT TO secure-network
```
docker network disconnect bridge payment
docker start --network=secure-network login-container
```
#### DOCKER FILE (BUILD DOCKER IMAGE STEPS)
```
FROM ubuntu:latest

SET THE WORKING DIRECTORY IN THE IMAGE
WORKDIR /app

COPY THE FILES FROM HOST FILE SYSTEM TO THE IMAGE FILE SYSTEM
COPY . /app
```
#### INSTALL THE NECESSARY DEPENDENCIES
```
RUN apt-get update && apt-get install -y python3 python3.pip
```
#### SET ENVIRONMENT VARIABLES
```
ENV NAME world
```
#### RUN A COMMAND TO START APPLICATION
```
CMD ["python3", "app.py"]
```


#### CHEAT SHEET 
https://www.hostinger.in/tutorials/docker-cheat-sheet?ppc_campaign=google_search_generic_hosting_all&bidkw=defaultkeyword&lo=9303798&gclid=CjwKCAjwlJimBhAsEiwA1hrp5j2AzuZ042LfWvLlvPU-j5wvLH-msb7EJOP4PGedSmsyau5AdosBhhoCyo8QAvD_BwE

#### LEARNING RESOURCE
https://github.com/iam-veeramalla/Docker-Zero-to-Hero


--------------------------------------------------------------------------------------------- DOCkERIZE ANGULAR APP
#### CREATE A FOLDER
```
mkdir 3
cd 3
```
#### CLEAN DOCKER IMAGES, CONTAINERS, VOLUMES AND NETWORKS
```
docker system prune
```
#### GIT CLONE
```
git clone https://github.com/Kumarabh/docker-angular-app-1.git
```
#### CD
```
cd angular-app
```
#### Build image from Dockerfile
```
docker build -t angular-app .
```
#### RUN IMAGE
```
docker run -d --name=angular-app -p 4200:80 angular-app
host (4200) 
nginx (80)
```

OPEN BROWSER AND HIT:- http://15.206.167.186:4200/

#### Dockerfile ( IT'S WORKING )

#### stage 1
```
FROM node:alpine as builder
WORKDIR /app
RUN npm cache clean --force
COPY package.json .
RUN npm install
RUN npm i @angular/cli@15.1.6
COPY . /app
RUN npm run build
```
#### stage 2

```
FROM nginx:1.21-alpine
COPY --from=builder /app/dist/angular-app /usr/share/nginx/html

```

--------------------------------------- USE FULL
#### Add user to docker group
```
sudo chmod -R 775 . 
sudo chown -R : .
```

















