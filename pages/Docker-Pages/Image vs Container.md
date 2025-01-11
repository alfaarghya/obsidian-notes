
![s7.png](Docker%20b32a6be1c4274eff9bed8fcd0dc65e0c/s7.png)

### **Docker Image**

A Docker image is a lightweight, standalone, executable package that includes everything needed to run a piece of software, including the code, a runtime, libraries, environment variables, and configuration files.

A good mental model for understanding a Docker image is to think of it as your codebase on GitHub. Just like how your codebase on GitHub contains all the necessary files and dependencies to run your application, a Docker image contains everything required to run a specific software or application.

Docker images are built from a set of instructions called a Dockerfile. The Dockerfile specifies the steps to create the image, such as installing dependencies, copying files, and setting environment variables.

### **Docker Container**

A Docker container is a running instance of a Docker image. It encapsulates the application or service and its dependencies, running in an isolated environment.

A good mental model for understanding a Docker container is to think of it as when you run `node index.js` on your machine from some source code you got from GitHub. Just like how running `node index.js` creates an instance of your application, a Docker container is an instance of a Docker image, running the application or service within an isolated environment.

Docker containers are created from Docker images and can be started, stopped, and restarted as needed. Multiple containers can be created from the same image, each running as an isolated instance of the application or service.

Here's an example command to create and run a container from the official `nginx` image:

```

docker run -d --name my-nginx-container -p 8080:80 nginx
```

This command creates a new container named `my-nginx-container` from the `nginx` image and maps the container's port `80` to the host's port `8080`. The `-d` flag runs the container in detached mode (in the background).

Once the container is running, you can access the Nginx web server by visiting `http://localhost:8080` in your web browser.

 To summarize:

- **Docker Image**: A lightweight, standalone package that contains everything needed to run a piece of software, similar to a codebase on GitHub.
- **Docker Container**: A running instance of a Docker image, encapsulating the application or service and its dependencies in an isolated environment, similar to running `node index.js` from a codebase.


## **Port mapping**

 The command `docker run -d -p 27018:27017 mongo` is used to run a MongoDB container and map the container's port to a different port on the host machine. Let's break down the different parts of this command:

1. `docker run`: This command is used to create and start a new container from a Docker image.
2. `d`: This flag runs the container in detached mode, which means it runs in the background and doesn't block the terminal.
3. `p 27018:27017`: This flag is used for port mapping. It maps the container's port `27017` (the default port for MongoDB) to the host's port `27018`. This means that you can access the MongoDB instance running inside the container from the host machine using the port `27018`.
    
    The syntax for port mapping is `-p <host_port>:<container_port>`. In this case, `27018` is the host port, and `27017` is the container port.
    
4. `mongo`: This is the name of the Docker image from which the container will be created. In this case, it's the official MongoDB image from Docker Hub.

![s8.png](Docker%20b32a6be1c4274eff9bed8fcd0dc65e0c/s8.png)

When you run this command, Docker will pull the `mongo` image (if it's not already present on your machine), create a new container from that image, and start the MongoDB server inside the container. The container's port `27017` will be mapped to the host's port `27018`.

This port mapping is useful when you want to access the service running inside the container from the host machine or other containers. Without port mapping, the service would only be accessible from within the container itself.

For example, if you have a Node.js application running on your host machine that needs to connect to the MongoDB instance, you can use the host's port `27018` as the connection URL (e.g., `mongodb://localhost:27018`).

> It's important to note that if the host port (27018 in this case) is already in use by another process, Docker will raise an error, and you'll need to choose a different host port for the mapping.
> 
