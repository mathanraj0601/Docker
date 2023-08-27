
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

 
