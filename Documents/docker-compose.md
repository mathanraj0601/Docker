# Docker Compose (mini project)
 Docker compose is when we need to run an entire application (backend, frontend and database ) at once

> Note : I am using [Voting-app](https://github.com/dockersamples/example-voting-app) which contains 5 different service running as seperate container

## Using docker run command

1. docker run --name redis redis : to run the redis service

1. docker run --name db postgres : to run the postgres service

1. docker built -t vote-app .

1. docker built -t worker-app .

1. docker built -t result-app .

1. docker run --link redis:redis --link db:db worker-app

1. docker run --link redis:redis -p 5000:80 vote-app

1. docker run --link db:db -p 5001:80  result-app

> Note for postgres try to give password and username as env using -e

## Using docker compose v1
We need to install docker-compose as it won't come default with docker.

```
redis :
    image : redis

db :
    image : postgres
     environment:
      - POSTGRES_PASSWORD  = password

vote-app
    built :./vote
    ports :
        - 5000:80
    links :
        - redis

worker-app
    built :./worker
    links :
        - redis
        - db

result-app
    built :./result
    ports :
        - 5001:80
    links :
        - db
```

The structure is simple the service name : the properties (that we mentioned in run command also)
> Note : Compose V1 support will no longer be provided after June 2023 and links proprety also deprecated

## Using docker compose v2
```
version: '2'
services:
    redis :
        image : redis

    db :
        image : postgres
        environment:
        - POSTGRES_PASSWORD  = password

    vote-app
        built :./vote
        ports :
            - 5000:80
        networks :
            - frontend

    worker-app
        built :./worker
        networks :
            - backend
            - frontend
        

    result-app
        built :./result
        ports :
            - 5001:80
        networks :
            - backend
networks
    frontend:
    backend:

```
Instead of link we go for network, The above format is applicable for version '3' aslo.
> Note : If we don't mention anynetwork docker itself create a network and connect all the containers and take care of DNS.