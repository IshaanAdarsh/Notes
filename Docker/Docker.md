# Docker:
- Docker is a tool for running applications in an isolated Environment
- Learning from -> https://www.youtube.com/watch?v=p28piYY_wv8

## Docker Container:
- Containers are an abstraction at the app layer that packages code and dependencies together. 
- It is the running instance of an image

<img width="369" alt="Screenshot 2023-12-22 at 11 13 57 AM" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/244426ac-e37f-4f09-b637-efa34928cbd4">

## Docker Image:
- Image is a template for creating an environment of your Choice, it contains everything your app needs to run.
- It contains OS, Software, App code
- Snapshot == version of image

<img width="770" alt="Screenshot 2023-12-22 at 11 56 05 AM" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/36e3ee17-3104-46a4-ab25-28e659c71ab3">

### Pulling an image:
```
docker pull xyz
```
This pulls the latest version of the image form [dockerhub](https://hub.docker.com)/

### Running container:
- Run a docker container
``` 
- Regular mode
docker run xyz:tag
// docker run nginx:latest

- Detached mode
docker run -d xyz:tag
// docker run -d nginx:latest
```

- Stop a docker container:

```
- Regular mode
cmd+c

- Detached mode
docker stop container_name[2]/ container_id[1]
```

- List number of containers:
```
docker container ls

// Good practice (preferred)
docker ps

CONTAINER ID[1] IMAGE          COMMAND                  CREATED         STATUS         PORTS     NAMES[2]
4e7f648b4b69    nginx:latest   "/docker-entrypoint.…"   4 minutes ago   Up 4 minutes   80/tcp    thirsty_diffie
```

### Exposing Port:
-  To make a reuest from the host(localhost) to the container.
-  localhost:8080 should map to port 80 of the container or multiple hosts to multiple posts.

#### Single port mapping:
```
docker run -d -p 8080:80 nginx:latest

docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         *PORTS                 NAMES
8118bb83815e   nginx:latest   "/docker-entrypoint.…"   2 seconds ago   Up 2 seconds   0.0.0.0:8080->80/tcp   exciting_ardinghelli
```
<img width="1436" alt="Screenshot 2023-12-22 at 12 19 18 PM" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/7c425785-f046-4957-8577-13a501b9e581">

#### Mapping multiple port:
```
docker run -d -p 3000:80 -p 8080:80 nginx:latest

docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                                        NAMES
22a1cffeeffb   nginx:latest   "/docker-entrypoint.…"   5 seconds ago   Up 4 seconds   0.0.0.0:3000->80/tcp, 0.0.0.0:8080->80/tcp   recursing_austin
```

<img width="1326" alt="Screenshot 2023-12-22 at 12 28 05 PM" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/6e0eaf9b-1bba-4160-a0e4-75a5f779f848">

### Managing Container:



