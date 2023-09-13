![image](https://github.com/mathanraj0601/Docker/assets/98396468/614b2a85-f888-42ca-96ff-fa651bd48b72)# Volume mapping 
-  Volume mapping involves storing the container instance data in the host (local machine). so that on running a new container of that docker image by mapping the folder in our host.
-  so that we can get the data from the folder in the host to start from where we left


  ## Demo Project on volume mapping Jenkins (a CI/CD tool)

Step 1: Creating a VM to work
  ![VM](https://github.com/mathanraj0601/Docker/assets/98396468/50072db0-0baa-418d-bc72-e92dda3cfef9)
Step 2: Installing Docker using the script in Centos machine and running the Docker service
```
Docker :
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker. sh
docker service:
sudo systemctl start  docker

```
![docker](https://github.com/mathanraj0601/Docker/assets/98396468/f3cb312e-70a4-4187-876d-592ef940e11d)

Step 3: Running Jenkins without volume and port mapping
```
docker run Jenkins/Jenkins
docker inspect image_id to get ip of the 
```
![image](https://github.com/mathanraj0601/Docker/assets/98396468/f258d0c0-207e-4c2c-9f24-aea0c50abd0a)
Jenkins dashboard :
![dashbroad](https://github.com/mathanraj0601/Docker/assets/98396468/859f907e-b7e5-48b2-aa79-23c12d93c595)
![image](https://github.com/mathanraj0601/Docker/assets/98396468/dba4dbf5-7eea-4f28-9288-cc2fe0c24480)

Step 4: Configure Username and password - stop the docker
```
docker stop image_id
```

step 5: Configure port and volume mapping

```
docker run -v /root/jenkins:/var/jenkins_home -p 8000:8000 Jenkins/Jenkins 
```


