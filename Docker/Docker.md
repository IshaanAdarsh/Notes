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
#### Run a docker container
``` 
- Regular mode
docker run xyz:tag
// docker run nginx:latest

- Detached mode
docker run -d xyz:tag
// docker run -d nginx:latest
```

#### Stop a docker container:

```
- Regular mode
cmd+c

- Detached mode
docker stop container_name[2]/ container_id[1]
```

#### List number of containers:
- ps only lists number of running containers.
```
docker container ls

// Good practice (preferred)
docker ps

CONTAINER ID[1] IMAGE          COMMAND                  CREATED         STATUS         PORTS     NAMES[2]
4e7f648b4b69    nginx:latest   "/docker-entrypoint.…"   4 minutes ago   Up 4 minutes   80/tcp    thirsty_diffie
```
- If we use -a suffix we can see all the containers, as when a container is stopped it's not deleted.

```
docker ps -a

CONTAINER ID   IMAGE          COMMAND                  CREATED       STATUS                   PORTS                                        NAMES
22a1cffeeffb   nginx:latest   "/docker-entrypoint.…"   7 hours ago   Up 45 seconds            0.0.0.0:3000->80/tcp, 0.0.0.0:8080->80/tcp   recursing_austin
8118bb83815e   nginx:latest   "/docker-entrypoint.…"   7 hours ago   Exited (0) 7 hours ago                                                exciting_ardinghelli
fbbfffe154dc   nginx:latest   "/docker-entrypoint.…"   7 hours ago   Exited (0) 7 hours ago                                                jolly_satoshi
4e7f648b4b69   nginx:latest   "/docker-entrypoint.…"   7 hours ago   Exited (0) 7 hours ago                                                thirsty_diffie
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
#### Delete a container:
- Use `docker rm`
- The container can't be running when you delete it, but to remove a running container you can pass `docker rm -f
_$(docker ps -aq)`
```
// Delete a single container
docker rm exciting_ardinghelli

// Delete all containers:
docker rm $(docker ps -aq)

// docker ps -aq -> lists all the container_id of all the containers
```

#### Naming Containers:
- We use the prefix `--name $xyz`
```
docker run --name website -d -p 3000:80 -p 8080:80 nginx:latest
```

#### `docker ps` formatting:
- We can format the content of the ps command using a preset format.
- Syntax: `--format`
```
//format used:
ID\t{{.ID}}\nNAME\t{{.Names}}\nImage\t{{.Image}}\nPORTS\t{{.Ports}}\nCOMMAND\t{{.Command}}\nCREATED\t{{.CreatedAt}}\nSTATUS\t{{.Status}}\n

// Command
docker ps -a --format="ID\t{{.ID}}\nNAME\t{{.Names}}\nImage\t{{.Image}}\nPORTS\t{{.Ports}}\nCOMMAND\t{{.Command}}\nCREATED\t{{.CreatedAt}}\nSTATUS\t{{.Status}}\n"

ID	1b3701106203
NAME	website
Image	nginx:latest
PORTS
COMMAND	"/docker-entrypoint.…"
CREATED	2023-12-22 19:35:54 +0530 IST
STATUS	Exited (0) 4 minutes ago

The better way to use format is to create a variable:
// Create a variable:
export FORMAT="ID\t{{.ID}}\nNAME\t{{.Names}}\nImage\t{{.Image}}\nPORTS\t{{.Ports}}\nCOMMAND\t{{.Command}}\nCREATED\t{{.CreatedAt}}\nSTATUS\t{{.Status}}\n"

// Run the command and call the variable
docker ps -a --format=$FORMAT
ID	1b3701106203
NAME	website
Image	nginx:latest
PORTS	0.0.0.0:3000->80/tcp, 0.0.0.0:8080->80/tcp
COMMAND	"/docker-entrypoint.…"
CREATED	2023-12-22 19:35:54 +0530 IST
STATUS	Up 4 minutes
```

### Docker Volumes:
- Allows sharing of data (Files & Folders) between
    - host and containers
    - Multiple Containers 
<img width="679" alt="Screenshot 2023-12-24 at 12 09 45 AM" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/ab8da3de-a334-423f-9a08-70ae17a99baa">
