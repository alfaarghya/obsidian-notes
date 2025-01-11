
![s9.png](Docker%20b32a6be1c4274eff9bed8fcd0dc65e0c/s9.png)

### **How to Write a Dockerfile**

A Dockerfile typically consists of two main parts:

1. **Base Image**: The first line in a Dockerfile specifies the base image to start from. This can be an official image from Docker Hub or a custom image you've built previously.
2. **Commands**: The rest of the Dockerfile contains a series of commands that are executed on top of the base image to create the desired environment for your application.

Here are some common commands used in Dockerfiles:

- `WORKDIR`: Sets the working directory for any subsequent instructions (`RUN`, `CMD`, `ENTRYPOINT`, `COPY`).
- `RUN`: Executes a command in a new layer on top of the current image and commits the results.
- `CMD`: Provides the default command to run when a container is started from the image.
- `EXPOSE`: Informs Docker that the container listens on the specified network ports at runtime.
- `ENV`: Sets an environment variable.
- `COPY`: Copies files from the Docker host to the Docker image.

### **Example Dockerfile**

Let's create a Dockerfile for the backend application from the provided GitHub repository: [https://github.com/100xdevs-cohort-2/week-15-live-1](https://github.com/100xdevs-cohort-2/week-15-live-1)

```

# Use the official Node.js image as the base
FROM node:18

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the port the app runs on
EXPOSE 3000

# Start the application
CMD ["npm", "start"]
```

Here's what each instruction does:

1. `FROM node:18`: Specifies the base image as the official Node.js 18 image from Docker Hub.
2. `WORKDIR /app`: Sets the working directory to `/app` inside the container.
3. `COPY package*.json ./`: Copies the `package.json` and `package-lock.json` files to the working directory.
4. `RUN npm install`: Installs the application's dependencies.
5. `COPY . .`: Copies the rest of the application code to the working directory.
6. `EXPOSE 3000`: Informs Docker that the container listens on port 3000 at runtime.
7. `CMD ["npm", "start"]`: Sets the default command to run when the container starts, which is `npm start` in this case.

###  **Building and Running the Docker Image**

 To build the Docker image from the Dockerfile, navigate to the directory containing the Dockerfile and run the following command:

```

docker build -t my-backend-app .
```

This command builds the Docker image and tags it with the name `my-backend-app`.

Once the image is built, you can run a container from it using the following command:

```

docker run -p 3000:3000 my-backend-app
```

This command runs a container from the `my-backend-app` image and maps the container's port `3000` to the host's port `3000` using the `-p` flag.

> By creating a Dockerfile, you can easily package your application and its dependencies into a Docker image, ensuring consistent and reproducible environments across different systems.
> 

### **Passing in env variables**

Docker allows you to set environment variables when running a container using the `-e` or `--env` flag. This is particularly useful when you need to provide configuration values or sensitive data (like database connection strings) to your application without hardcoding them in your codebase.

Here's an example of how you can pass an environment variable to a Docker container:

```
docker run -p 3000:3000 -e DATABASE_URL="env_DB_url" my-image-name
```

Let's break down this command:

- `docker run`: This command is used to create and start a new container from a Docker image.
- `p 3000:3000`: This flag maps the container's port `3000` to the host's port `3000`. This is useful when your application listens on a specific port, and you want to access it from the host machine.
- `e DATABASE_URL="postgres://..."`: This flag sets an environment variable called `DATABASE_URL` inside the container. The value provided after the `=` sign is the actual value of the environment variable. In this case, it's a PostgreSQL connection string.
- `my-image-name`: This is the name of the Docker image from which the container will be created.

In the example command, we're setting the `DATABASE_URL` environment variable inside the container with a PostgreSQL connection string. This connection string can then be accessed and used by your application running inside the container.

To access environment variables in a Node.js application, you can use the `process.env` object. For example:

```jsx
const databaseUrl = process.env.DATABASE_URL;
// Use the databaseUrl variable to connect to the database
```

> By passing environment variables to Docker containers, you can separate configuration values from your application code, making it easier to manage and deploy your application in different environments (e.g., development, staging, production) without modifying the codebase.
> 


# Dockerfile

```docker

# Use the official Node.js image as the base
FROM node:18

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the port the app runs on
EXPOSE 3000

# Start the application
CMD ["npm", "start"]
```