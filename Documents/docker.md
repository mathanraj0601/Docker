
## What is docker?

- Docker is an application that helps us  to run our application in an isolated way (As containers) i.e. no dependencies or conflicts of libraries and is going to affect the application running 

- It avoids the situation of “It works on my computer but not on yours.“


## We can do the same with virtualization (Virtual machine) then why docker?

- Yes we can run an application in a VM in an isolated manner but it affects the system performance greatly 

- For example, consider running three applications in three virtual machines in a single host will require (the base OS / Hypervisor ) to boot it up which will result in a delay and three  virtual machines have separate  storage and require more resources and we need to set the application dependencies in each virtual machines manually that is a lot of time and resource-consuming process 
 
- Hypervisors are software used to manage virtual machines in the Computer system
  
- Docker came to resolve this issue. Docker is Os Kernel dependent that is we can run any Linux distros in one kernel

- Docker runs an application in the form of an image. An image is a template of an application We can download this image from the Docker registry hub which is like GitHub and simply run the instance using Docker CLIi with the command “docker run” The docker will take care of the OS and dependencies the application needs and run the application in one command/ click( if docker desktop)


## What is a Docker image?

- It is a file that has  all dependencies, os, other services, and source code of our application


## What are Docker containers?

- The running instance of the docker image is handled by the docker host.


## Docker Installation 

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

- docker rm *image-name* : To remove image from the Process status (Removing the container from the system not the actual image )

>  Note :Before Removing the images we need stop the image,
Removing the container delete all the data inside the container


- docker images :  to list all the images in our host

- docker rmi : docker remove image used to remove image from the host.

- docker pull : used to pull the image from docker hub
> note docker run - start and pull the image from hub if not in host

```
Docker is used mostly for running services like redis, webserve etc., which implies that it run/ excute  something . if we run a os image it don't have anything to execute so it will start and stop at the moment to make it alive for shorter time period we can use sleep command along the with 
run.Meanwhile, if we need to execute any command we can use docker exec 

```
- docker run ubuntu sleep 5 : Make the ubuntu container run for 5 seconds by giving it commands to executes

- docker exec *image-name* *command* : It will exec the command in the container (execute command in terminal of the container )



```
If you run a image you will notice that it will not allow us to run any more command we need to stop the container by using "Ctrl+C" in same terminal or open a new terminal and stop this container or start new container . This is because we are running the container in foreground mode

There are two mode to run a Container
- Foreground mode or attached mode
- Background or Detached mode


```
- docker run -d *image-name* :  Run the image in detached / background mode ( "d" - detached )

- docker attach *image-name* or *container-id* : make the detached mode container to attach ( now we can able to communicate to the instance using standard output like terminals)

```
Docker tags are the version of the images by default if we pull the image without mentioning anything other than the image name it will have latest .

For particular version, we need to append version as prefix to image 

example : docker run redis > latest tag
          docker run redis:4.0 > 4.0 version tag
```

```
If we have some application which need a input to executed something simple example will be a app which take your name by asking "Enter you sweet name" and display it in standard output "welcome your-name"

Directly running the containeer will not get any input and simple output "welcome" so we need to run in interactive mode to give input

```

- docker run -i *image-name* : To run the image in interactive mode
> It will only show blank space and "Enter your name "
as in interactive mode it wait for some standard input only

- docker run -it *image - to  run the image in interactive more along with terminal 
> it will display the input message to get input as we now have a terminal to interact rather than simple input 

```
Docker container itself expose port so that our host can interact with it but other machine can't make a connection because we don't have any way opened for other machine to  connect with it .

for that we map the port of docker conatiner with our local machine container so that other machine can acesss it using the host machine IP along with port number

docker port before mapping the ip is container-ip:port-number 
(local access)

Note : To get the default ip of container run docker inspect 

docker port after mapping get the host ip example : 198.8.8.8:port-number

 we can specify the docker port too example docker run -p 8000:6000 nginx

```

 - docker run -p *host-port* - *docker-port*  *image-name* will run the docker in specified port number to make a external connection.

```
Volume mapping :    The use of volume mapping that we can able to store the data of container into our host so that if we remove the container on re running we can able to get the data from here

```
- docker run -v *host-directory* : *container:directory* : used to connect the directories of host and container so that the data will be stored permenantly in host and temporarily in container

- docker logs *image-name* : used to see all the logs and error of the image in standard output

- docker inspect *image-name* : used to see details of the images (running container)

```
Creation docker images

the dockerfile consist of command like from,run,expose etc and arguments for that 

For example

From OS / parent image
Run dependencies
Copy source/code (where to copy and where to paste)
Entry point for application

Note : From should be the first line in the docker file

Docker file are build in a layered manner that each command is executed on top opf other so the change of each command are stored over other this enable us to run the build command
from where it failed if failure or where it get changed as its use the caches in building the previous version that enable us to save time

```

- docker build *docker-txt-file* -t *name-of-the-image* : will build a image in layered manner with the name specified using the -t option that is tag if specified like *name-of-the-iamhe:tag* it wil take that or default it is latest

- docker login : allow to login into remote docker hub repositories

- docker push - enable to pubish the command to hub
> Note : Docker push default pushes in library organization which is meintained by docker and we don't have acces to it
we need to make the name of the image with our docker account name like below to push to docker hub .(for normal account we can have only one private repo)

- docker build *docker-txt-file* -t *docker-hub-account/name-of-the-image*

```
Evironmental variable : if we need to give our image some value which changes it better to have as env variable so that it can get from the os using os.environ.get("env_ name") and we can assign it to os by export env_name=*value in case of linux machine or we can mention the run command itself using option -e
```

- docker run -e *env_name*=*value*  *image-name* --name *user-defined-name*

> Note: using --name we can give the running instance of the image our own name

```
Entrypoint, Command , Expose 

entrypoint is the first command to be executed in the container

eg: ENTRYPOINT python app.py

we can mention it as json array 
ENTRYPOINT ["command" ,"argument"] 
eg: ENTRYPOINT ["python" ,"app.py"] 

the difference is that if we pass some args in the time of docker run command it will get appended in case opf json array and overwritten if mention in text


so image have cmd in it implies that it get append to entry point and run in the container as first if entry point is mentioned otherwise it will simply what is mentioned in it

cmd aslo inside an json array eg: cmd["5"]

it act as default value for the entrypoint command 

there may br situation where need the argument from the user so we make the entry point as ENTRYPOINT ["sleep" ] (has only command and not parameter) if we run it directly it will through error like no value for the command so to give default value we use cmd ["5"] if user enters something it will get overwritten 


```
- docker run *image-name* *arguments* : it will run the image with argument that your are giving as by appending with entrypoint

- docker run *image-name* *command-argument*  : it will run a image with the  entrypoint as a whole overwritten
> Note : For making it more clear we can use the below options

- docker run *image-name* --entrypoint *command-argument* : it will run the container with what you mentioned as a entry point



 

