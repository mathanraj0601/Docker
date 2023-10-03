
## What is docker?

- Docker is an application that helps us  to run our application in an isolated way (As containers) i.e. no more dependencies or conflicts of libraries is going to affect the application running 

- It avoids the situation of “It works on my computer but not on yours.“


## We can do the same with virtualization (Virtual machine) then why docker?

- Yes, we can run an application in a VM in an isolated manner but it affects the system performance greatly 

- For example, consider running three applications in three virtual machines in a single host will require (the base OS / Hypervisor ) to boot it up which will result in a delay and three  virtual machines have separate  storage and require more resources and we need to set the application dependencies in each virtual machines manually that is a lot of time and resource-consuming process 
 
- Hypervisors are software used to manage virtual machines in the Computer system
  -  Hypervisor involves two type 
    - Bare metal hypervisor: lies between hardware and vm
    - Hosted hypervisor : lies between hostel os and vm

- Docker came to resolve this issue. Docker is Os Kernel dependent that is we can run any Linux distros in one linux kernel similarly for other OS.

- Docker runs an application in the form of an image. An image is a template of an application We can download this image from the Docker registry hub which is like GitHub and simply run the instance using Docker CLI with the command “docker run” The docker will take care of the OS and dependencies the application needs and run the application in one command/ click( if docker desktop)


## What is a Docker image?

- It is a file that has all dependencies, os, other services, and source code of our application


## What are Docker containers?

- The running instance of the docker image which is handled by the docker host is called docker container.


## Docker Installation for linux
Installing Docker using the script in Centos machine and running the Docker service

```
Docker :
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker. sh
docker service:
sudo systemctl start  docker
```
> Note : there are lot of way to install docker but the easiest way is to run the above script it will take care of the dependencies by itself

## Docker Command

- docker run *image-name* : to run a instance of a image / starting a container (if not localy present it pull from the docker registry hub).\
 example : docker run nginx

- docker ps : docker process status will give the list of running instance / container

- docker ps -a : will give the list of all container in an system . The list consist of 7 Columns value there are :

  - Container id : Unique value for each container
  - Image : Which docker image eg : nginx  
  - Command : it is the initial command executed inside the container
  - created : when the container was created
  - Status : current status of the container example: exited, up etc.,
  - ports : the port exposed for container ( or ) The port mapped between host(our computer) and container
  - Name : Name of the container ( Auto-generated  or User-Assigned)

- docker stop *image-name* : to stop the container or make the status to exited.

- docker rm *image-name* : To remove image from the Process status (Removing the container (running image) from the system not the actual image )

>  Note :Before Removing the images we need stop the image, Removing the container delete all the data inside the container

- docker images : to list all the images in our host

- docker rmi : docker remove image used to remove image from the host.

- docker pull : used to pull the image from docker hub

> note docker run - start and pull the image from hub if not in host

Docker is used mostly for running services like redis, webserve etc., which implies that it run/ excute  something . if we run a os image it don't have anything to execute so it will start and stop at the same time.

To make it alive for shorter time period we can use sleep command along the with 
run.Meanwhile, if we need to execute any command we can use docker exec.

- docker run ubuntu sleep 5 : Make the ubuntu container run for 5 seconds by giving it commands to executes

- docker exec *image-name* *command* : It will exec the command in the container (execute command in terminal of the container )


If you run a image you will notice that it will not allow us to run any more command we need to stop the container by using "Ctrl+C" in same terminal or open a new terminal and stop this container or start new container . This is because we are running the container in foreground mode

There are two mode to run a Container
- Foreground mode or attached mode
- Background or Detached mode


- docker run -d *image-name* :  Run the image in detached / background mode ( "d" - detached )

- docker attach *image-name* or *container-id* : make the detached mode container to attach ( now we can able to communicate to the instance using standard output like terminals)

Docker tags are the version of the images by default if we pull the image without mentioning anything other than the image name it will have latest .

For particular version, we need to append version as prefix to image 

example : docker run redis : run redis latest version tag
          docker run redis:4.0 : it will run the redis 4.0 version tag

If we have some application which need a input to executed something for example : app which take your name by asking "Enter you sweet name" and display it in standard output "welcome your-name"

Directly running the containeer will not get any input and simple output "welcome" so we need to run in interactive mode to give input

- docker run -i *image-name* : To run the image in interactive mode
> It will only show blank space and not "Enter your name " if you have in the program

as in interactive mode it wait for some standard input only and no standard output

- docker run -it *image-name* - to  run the image in interactive more along with terminal 

> it will display the input message to get input from user as we now have a terminal to interact rather than simple input 


Docker container itself expose port so that our host can interact with it but other machine can't make a connection with running image because we don't have any way opened for other machine to  connect with it .

for that we map the port of docker container with our local machine container so that other machine can acesss it using the host machine IP along with port number

docker port before mapping the ip is container-ip:port-number (local access from host system browser). After after mapping get the host ip example : *host-ip*:port-number

example : docker run -p 8000:6000 nginx : run a nginx image with host port 8000 and docker port 6000 so now we can access the running container from the outside of host using *host-ip*:*port-number*

> Note : To get the default ip of container run docker inspect 

we can specify the docker port too example 

- docker run -p *host-port* - *docker-port*  *image-name* will run the docker in specified port number to make a external connection.

Volume mapping : The use of volume mapping that we can able to store the data of container into our host so that if we remove the container on re running we can able to get the data from here

- docker run -v *host-directory* : *container:directory* : used to connect the directories of host and container so that the data will be stored permenantly in host and temporarily in container

- docker logs *image-name* : used to see all the logs and error of the image in standard output

- docker inspect *image-name* : used to see details of the images (running container)


Creation docker images

the dockerfile consist of command like from,run,expose etc and arguments for that 

For example

From OS / parent image
Run dependencies
Copy source/code (where to copy and where to paste)
Entry point for application

Note : From should be the first line in the docker file

- FROM : base image / os

- RUN : to run the dependency files

- COPY : for copy source to the build image

Docker file are build in a layered manner that each command is executed on top of other so the change of each command are stored over other this enable us to run the build command from where it failed if failure or where it get changed as its use the caches in building the previous version that enable us to save time

> Docker enginer store the layered in cache and help to use for next build


- docker build *docker-txt-file* -t *name-of-the-image* *path-to-docker-file*: will build a image in layered manner with the name specified using the -t option that is tag if specified like *name-of-the-iamhe:tag* it wil take that or default it is latest

- docker login : allow to login into remote docker hub repositories

- docker push - enable to pubish the command to hub

> Note : Docker push default pushes in library organization which is meintained by docker and we don't have acces to it we need to make the name of the image with our docker account name like below to push to docker hub .(for normal account we can have only one private repo)

- docker build -t *docker-hub-account/name-of-the-image* *path-to-docker-file*

> Note : it will take the default file DockerFile in the current directory

- docker build -t *docker-hub-account/name-of-the-image* -f *name-of-the-docker-file* *path-to-docker-file*

> note : -f used to specify docker file name if we named somewhat else

Evironmental variable : if we need to give our image some value which changes it better to have as env variable so that it can get from the os using os.environ.get("env_ name") and we can assign it to os by export *env_name*=*value* in case of linux machine or we can mention the run command itself using option -e

- docker run -e *env_name*=*value* *image-name* --name *user-defined-name*

> Note: using --name we can give the running instance of the image our own name

Entrypoint, Command , Expose 

- ENTRYPOINT is the first command to be executed in the container

eg: ENTRYPOINT python app.py

we can mention it as json array 
ENTRYPOINT ["command" ,"argument"] 
eg: ENTRYPOINT ["python" ,"app.py"] 

The difference is that if we pass some args in the time of docker run command it will get appended in case of json array and overwritten if mention in text

so image have cmd in it implies that it get append to entry point and run in the container as first if entry point is mentioned otherwise it will simply what is mentioned in it

- CMD aslo inside an json array eg: cmd["5"]

it act as default value for the entrypoint command if no entry point specified it will run by default

there may br situation where need the argument from the user so we make the entry point as ENTRYPOINT ["sleep" ] (has only command and not parameter) if we run it directly it will through error like no value for the command so to give default value we use cmd ["5"] if user enters something it will get overwritten 

- WORKDIR : to chance the flow of the command to new repo / location inside the container (if folder not found it will created during runtime)

eg: WORKDIR /app : the docker file build which switch to this repo and run command mentioned below the workdir

- ENV : to set environment variable for that image

> Note : env is assigned only to that image it different from docker run -e which we pass dynamically

- docker run *image-name* *arguments* : it will run the image with argument that your are giving as by appending with entrypoint

- docker run *image-name* *command-argument*  : it will run a image with the  entrypoint as a whole overwritten
> Note : For making it more clear we can use the below options

- docker run *image-name* --entrypoint *command-argument* : it will run the container with what you mentioned as a entry point

- docker run --link *container-name*:*the name specified in the container to access the resource* *image-name*

link is used to link container to one another in default bridge network we can link by specifying the container-name which we need to connect : the name that we use in out container to access it ( it will create a record in the etc/hosts folder with a key value pair of ip of the container we need to access and the name we mentioned )

example :
 - docker run redis -- name db : the container we need to access
 - docker run ngnix --link db:ndb : the container from which we access the redis

 now nginx will have ip of redis container with ndb as record in etc/hosts

> Note if *container-name*:*name-we-mentioned-inside-the- container* are same then we mention only once *container-name*

docker run nginx --link db:db
or
docker run nginx --link db

> Note : --link is deprecated

Docker Compose
using docker run we can able to run a single image at a time. But imagine we have a entire application which have db, web server and application server so we need to run the image using docker run three times.It's time consuming as we need to do that same manual process in each machine to bring up the application at the same time we need to create link between this container to make talk to them.

But to overcome this we use docker-compose which is a configuration file written in yaml (an type of markup language) so by running the compose yaml file we can run entire application at once  by docker compose file

docker compose file maintain the configuration as a dictionary that is key-value pair


docker-compose file consist of three version :
  - docker-compose v1 : it allows mention the all run command in one area but in different format. The version 1 has the following properties : image, built,ports, links ,etc.,

```
  Example:

  user-defined-image-name : 
    image : *actual-image-name* 
    or
    built : *path-for-dockerfile-to-built*
    ports :
      - *host-port*:container-port*
    links :
      - *container-name*:*the name specified in the container to access the resource*

```


- docker-compose v2 : it has all the feature of v1 but also allows us to create network and isolate containers traffic using the properities networks

For docker-compose v2 we need mention the version:2 in the startinig of the compose file and at the same time we need to mention all the container inside the services properities and allows us to run the container in a required way.


```
Example:
version: 2
services :
  user-defined-image-name : 
    image : *actual-image-name* 
    or
    built : *path-for-dockerfile-to-built*
    depends_on : *the container it need to run*
    network - *name-of-network*
networks :
  - *name of the network*

```

The network will create a seperate network which is different from the default bridge network thus we can create isolated network.

 - docker compose v3 : enable us to orchustrate using docker swarm 
 

- docker compose -f *name-of-docker-file* up : to run a yaml file which has other than docker-compose as file name. 

In version 3, each project will run with a name prefix by the folder it in example if the folder is repo then repo_*the-name-in-compose-file* to avoid naming conflicts with other compose projects

- docker compose up -d : to run in detached mode

- docker compose down : to stop entire application

## Docker working

- Docker Engine : the host in which the docker installed is called as Docker engine
- Docker Engine has 
  - Docker CLI : Command line to interact with docker deomon
  - Rest API : Interface between program,cli and Docker deomon to execute the request
  - Docker Deomon : The image we create, pull, run are executed here.

## How docker main isolation between containers

Though all container share the common resources i.e. host such as cpu,memory etc., Docker achieve this isolation by namespace to isolate workspace of container (directory /file of that container)

In real world each process in machine/ environment start with pid =1  and follows the number
Docker/container process aslo come under this and take some pid >=1
But Container run isolately right then the pid of the container shouold start with pid =1 and so on

Yes Docker create seperate pid for container within itself and seperate pid in the host to actually process and map them bith which is called namespaces thus maintaining isolation

The docker maintain namespaces for
- inter-process
- process
- network
- UNIX Time-Sharing
- Mount   

> Note : There is no restriction for container access to resource by default in docker they can utilize entire resource if we need to restrict the access we can use control groups

## Control Groups
- It is the feature of linux kernel use to restrict resource access in docker
For example 
- docker run --cpus=0.5 *image-name* : ask the container to use at maximum of 50% of the host resource
- docker run --memory-100 *image-name* : ask container to use at max 100mb of memory

## Docker file system

- Docker store all the data in the file location /var/lib/docker
- This folder consist of sub-directories
  - storage driver folder eg:aufs
  - volumes 
  - images
  - containers

### Docker images and container folder :

- Docker the data related to image and container information here
- There are two layer created when we run a image 
    - Readonly layer
    - Container layer
- When we build a image we built as a layered manner so that docker re use the build cache when rebuilding the same image or  we have second image that follows most of the step in the first image thus reduce building time by using the first image caches

#### Readonly layer
- When we run a container its layer which has the actual image where we can't modify anything. it's more or like class in OOPS. 

#### Container layer
- It's a layer created by docker on top the readonly layer when we run a image. So the changes we a making newly or modifying the image will be tracked here it will alive untill the image in running status.  it's more or like object in OOPS.

Example : Conside a linux os image when we run and create a file using touch it is actually in the container layer so when we stop and re-run the file disappear. To over come this loss of data in case of crash we go for mount

### Docker bind mount and volume mount

- We do volume mapping to persist the data of container in host. There are two type
  - Volumes : we can create a volumes in the docker file system using docker volumes create *volume-name*. it will be created in /var/lib/docker/volumes as folder.We can simple mention the volume while running docker run -v *volume-name*:*container-storing-folder* *image-name* .no need to mention path of volumes
  - bind : when we create the mapping / mount other folder or other location then volumes we need to mention the actual path.it is called bind mount example : docker run -v *path-to-store-data*:*container-storing-folder* *image-name*

- docker run -v  *volume-name* or *path-to-store-data* :*container-storing-folder* *image-name* : is the traditional way od mounting folder
- docker run --mount type="*volume* (or) *bind*",source="*volumes* (or) *path",destination="*container-storing-folder*"  *image-name* : New or updated version for mounting folder

## Docker network 

- Docker network has three types
  - bridge
  - none
  - host

### Bridge Docker network

- Bridge network : A default network created by docker. Any container we run it get connected to this brigde network.This network  default assigned ip is 17.17.00.00/16 (series). The container in this bridge network can talk to each other but not with external internet.

- None network : A network in which container can't talk with another and also external internet.In simple word, isolated

- Host : A network which connect container to host network and container can expose it default port to external internet.(with out port mapping in case of default network)

> Note this default network create a DNS server at 127.0.0.1 (localhost) with  host name and assigned ip as key-value pair

### Custom network

- If we need group of container to specific network and isolate them . we can by creating a network

- docker network create --driver:*bridge (or) any other types* --subnet=*ip-range* --gateway-*starting-address-of-ip-range* *network-name*

- docker network ls : to list network

- docker network rm *network-id* : to delete network

- docker network inspect *network-id* : to inspect network details

- Network table has following columns
 - name
 - network-id
 - driver : type of network
 - scope : local (with in host) or global(across host).

> Note : Default-gateway help to communicate with external network

### Registry

- We use registry  such as dockerhub to store image in cloud
- There are two types of registry private and public eg: dockerhub - public, amazon registry or internal private registry - private registry
- The above mentioned registry are third parties
- If we need to create a registry in our own on-prem we can do that by a image in docker hub called registry-2 by default listen to port 5000:
- Docker by istelf when we pull or push it look in dockerhub by default if we need to change the registry we can do that by changing the config.json file of docker
- Another method is to mention the registry in tag of image
- docker image tag *image-name* *registry-link/image-name*

We can now push and pull  the tagged image to our own registry 

## Docker in Window

- As we know docker is kernel dependent we can run container based in it's base image os and kernel.We can't run linux container in window as kernel differs.
- For window there are window toolbox and window desktop
- window toolbox which has
  - oracle virtual box (vm)
  - docker (installed in vm)
  - GUI for docker

- window desktop
  - microsoft hyper -v (native vm)
  - docker (installed in vm)

We can now able to create window based container using the base image of window server core or nano server(a most light weight) image
- We can run image in two ways on :
  - Window hyper -v platform : where each container has a small kernel with it (a very light weight vm) on host kernel.
  - window server platform : where each container run direcly on kernel

## Docker in MAC

- As we know docker is kernel dependent we can run container based in it's base image os and kernel.We can't run linux container in mac as kernel differs.
- For mac there are mac toolbox and mac desktop
- mac toolbox which has
  - oracle virtual box (vm)
  - docker (installed in vm)
  - GUI for docker

- mac desktop
  - hyperkite (native vm)
  - docker (installed in vm)

> Note : docker can be runned in mac and window in same manner but the underlying virtual machine hypervisor is different.

## Docker Swarm

Consider if we need to run our application 1000 times we need to run the docker run that much time and if any one of them failed we need to monitor manually and again run it. If the docker host itself failed we need to create another machine , install docker and run all the application.

To overcome this issue orchestration tool like docker swarm come to play (docker swarm is native to docker)

- Docker swarm will create a cluster ( set of node that has docker init and make a node among them as master and other as worker)
- Master will take care of running our application across worker, creating new node if one failed, advanced network among them and load balancing
- Any command like " docker run --replicas=100 *image-name* " in master will create this instance distributed across the workers
- To setup a node as manager run docker swarm init
- To setup the work run docker swarm join --token *token-generated-by-master*

> There are other orchestrator like mesos, kubernetes which are advance then docker swarm and provide auto scaling .

## Kubernetes

- Another orchestrator by Google now currently in CCNF.

- It aslo have the same master, worker node and cluster concept
- It has its own cli and tools. The component of kubernetes are
  - etcd : key-value store for cluster configuration and state accross all node in a distributed manner.
  - server api : fronted of kubernetes through which user can interact
  - kubelet : a agent to manage node to behave as expected
  - scheduler : for creating a new node / service and place in a proper location / nodes.
  - container run-time : docker engine or some other container platform
  - controller : brain behind the kubernetes to monitor node/service failure and re span them.

> Dedicated cli like kubectl can help us to do what we did in docker swarm and more.

