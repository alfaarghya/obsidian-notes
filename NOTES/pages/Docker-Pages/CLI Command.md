

### docker pull

```docker
docker pull <image_name>
```

### docker run

#### **1. run a docker container**

```docker
docker run <image_name>
```

#### **2. port mapping** - it’s used to expose the port of the docker container for our use

```docker
docker run -p <our_port>:<container_port> <image_name>
```

#### **3. detach mode** - it frees the terminal

```docker
docker run -d <image_name>
```

#### 4. Passing environment variable

```docker
docker run -e <DATABASE_URL="connection string"> <image_name>
```

#### **5. docker container name** - name the docker container

```docker
docker run --name <coontainer_name> <image_name>
```

#### **6. Attach a volume to a docker container**

```docker
docker run -v <volume_name>:<path_to_store> <image_name>

# example - 
docker run -v DB_volume:/data/db -p 27017:27017 mongo
```

#### 7. Run container in a network

```docker
docker run -p <our_port>:<container_port> --name <coontainer_name> --network <network_name> <image_name>

#example - 
docker run -p 27017:27017 --name mongoDB_Server --network backen-network mongo
```

> as we are using `the` name of a container, now our DB connection URL look`s` like this - `'mongodb://mongoDB_server:27017/myDatabase'` 

###  docker ps

#### 1. see the current container running

```docker
docker ps 
```

#### 2. see all of the containers in the  system

```docker
docker ps -a
```


### docker images
see all of the images in our docker system

```docker    
docker images
```

### docker kill
kill or turn off a certain container that is running

```docker
docker kill <container_id>
```

### `docker rmi`
#### 1. remove a docker image

```docker
docker rmi <image_name>
```

#### 2. remove a docker image forcefully

```docker
docker rmi <image_name> --force
```

### docker build
**build a docker image -** for this we must have a `Dockerfile` in our code base

```docker
docker build -t <our_docker_image_name>:<tag> .
```

> `-t` means tag, we may have a different different versions of the same image, and for that we must give a tag to identify different images.
for example - `docker build -t backend-app:1.0.0 .`

### docker push
it’s used to push a docker image from locally to the docker hub

```docker
docker push <username>/<docker_image_name>:<tag>
```

### docker exec
it’s used to go into the file system of a current container

```docker
docker exec -it <container_id> <path/to/dicrectory>

#example - 
docker exec -it e699296f4261 /bin/bash
```

### docker volume
volume is mostly used in DB. 
when we kill a container, all the data the container carries also gets deleted permanently
So to avoid this problem, we attach a `volume` so that if our container gets deleted out data must stay

```docker
docker volume create <volume_name>
```

### docker network
when we have 2 container running(`backend-app` & `mongo-DB`) but we need those containers to communicate with each other. then we need to add them to the same network so they can communicate

```docker
docker network create <network_name>
```
