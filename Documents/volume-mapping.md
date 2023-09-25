# Volume mapping
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
```
Jenkins (initial setup) :
```
![dashbroad](https://github.com/mathanraj0601/Docker/assets/98396468/859f907e-b7e5-48b2-aa79-23c12d93c595)
```
Jenkins plugins (initial setup) :
```
![image](https://github.com/mathanraj0601/Docker/assets/98396468/dba4dbf5-7eea-4f28-9288-cc2fe0c24480)

Step 4: Configure Username and password - stop the docker
```
docker stop image_id
```

step 5: Configure volume mapping

```
docker run -v /root/jenkins:/var/jenkins_home  Jenkins/Jenkins 
```
![volume mapping](https://github.com/mathanraj0601/Docker/assets/98396468/78f95f38-49f1-40bd-93fe-7cb68046e0f7)
> Note: sometimes you may get a permission denied error to overcome it use  docker run -v /root/jenkins:/var/jenkins_home -u root  Jenkins/Jenkins  run the docker images a user root by adding(-u root)

step 6: Configure port mapping along with volume mapping (the Image below is the browser in my host machine)

```
docker run -p 50000:50000 -p 8080:8080 -v /root/jenkins:/var/jenkins_home  -u root Jenkins/Jenkins

```
![port mapping](https://github.com/mathanraj0601/Docker/assets/98396468/1df7fd6a-2bfe-4464-ab18-2d579bea3e92)
note > Vm should be in NAT with port forwarding or bridge network (for window machine if we can't reach the IP  because of firewall, try to create inbound rules in Firewall Defender)


