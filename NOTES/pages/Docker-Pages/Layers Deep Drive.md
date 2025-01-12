
### **How Layers are Made**

1. **Base Layer**:
The base layer is the starting point of an image, typically an operating system (OS) like Ubuntu, Alpine, or any other base image specified in a Dockerfile. This base layer provides the foundation for the subsequent layers.
2. **Instruction Layers**:
Each instruction in a Dockerfile creates a new layer in the image. These instructions include commands like `RUN`, `COPY`, `ENV`, and others, which modify the filesystem by installing packages, copying files from the host to the container, setting environment variables, or making other changes. Each of these modifications creates a new layer on top of the previous layer.


### Here's an example of how layers are created in a Dockerfile:

```

# Base layer
FROM ubuntu:20.04

# Instruction layer 1
RUN apt-get update && apt-get install -y python3

# Instruction layer 2
COPY . /app

# Instruction layer 3
RUN pip3 install -r /app/requirements.txt
```

 In this example, each `RUN` and `COPY` instruction creates a new layer on top of the previous one.

1. **Reusable and Shareable**:
Layers are cached and reusable across different images, which makes building and sharing images more efficient. If multiple images are built from the same base image or share common instructions, they can reuse the same layers, reducing storage space and speeding up image downloads and builds.
2. **Immutable**:
Once a layer is created, it cannot be changed. If a change is made, Docker creates a new layer that captures the difference. This immutability is key to Docker's reliability and performance, as unchanged layers can be shared across images and containers.


![https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fe775d1b9-f2e0-4b55-9149-f279a6cf9ab8%2FUntitled.png?table=block&id=503ad8b1-685c-46f6-9a07-92c292075a79&cache=v2](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fe775d1b9-f2e0-4b55-9149-f279a6cf9ab8%2FUntitled.png?table=block&id=503ad8b1-685c-46f6-9a07-92c292075a79&cache=v2)

### **Benefits of Layers**

 The layered architecture of Docker images provides several benefits:

1. **Efficient Storage**: By reusing and sharing layers across images, Docker can significantly reduce the storage space required for multiple images, as only the unique layers need to be stored.
2. **Faster Image Builds**: When building an image, Docker can reuse cached layers from previous builds, reducing the time and resources required for subsequent builds.
3. **Faster Image Distribution**: Since layers are shareable, Docker only needs to transfer the unique layers when distributing an image, resulting in faster image downloads and deployments.
4. **Version Control**: Each layer represents a specific set of changes, making it easier to track and roll back changes if necessary.
5. **Portability**: Docker images are portable across different environments and platforms because they encapsulate all the necessary dependencies and configurations within their layers.

> By understanding the layered architecture of Docker images, developers can optimize their Dockerfiles, leverage layer caching, and take advantage of the efficiency, speed, and portability benefits that Docker provides.
> 

## **Practically Understanding Layers**

 Let's analyze the layers created during the Docker build process for the simple Node.js application.

**Dockerfile:**

```

FROM node:18-alpine

WORKDIR /app

COPY package.json .
RUN npm install

COPY . .

CMD ["node", "index.js"]
```



**Build Logs:**

![s10.png](Docker%20b32a6be1c4274eff9bed8fcd0dc65e0c/s10.png)

![https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fe0969975-b5fd-4db6-a108-a5db4178f16b%2FUntitled.png?table=block&id=6acf62cf-4824-4e74-b12a-c64124cae388&cache=v2](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fe0969975-b5fd-4db6-a108-a5db4178f16b%2FUntitled.png?table=block&id=6acf62cf-4824-4e74-b12a-c64124cae388&cache=v2)

**Observations:**


1. **Base Image Layer**: The first layer is created from the base image specified in the `FROM` instruction. In this case, it's `node:18-alpine`, which is a lightweight Alpine Linux image with Node.js pre-installed. This layer serves as the foundation for the subsequent layers.
2. **`WORKDIR` Layer**: The `WORKDIR` instruction sets the working directory for the subsequent instructions in the Dockerfile. It creates a new layer on top of the base image layer. In this example, the working directory is set to `/app`.
3. **`COPY` Layer**: The `COPY` instruction is used twice in the Dockerfile. Each `COPY` instruction creates a new layer that adds files from the host system to the image filesystem.
    - The first `COPY` instruction copies the `package.json` file to the working directory (`/app`).
    - The second `COPY` instruction copies the rest of the application files (`.`) to the working directory.
4. **`RUN` Layer**: The `RUN` instruction executes a command inside the image and creates a new layer with the results. In this case, `RUN npm install` installs the dependencies specified in the `package.json` file, creating a new layer with the installed packages.
5. **`CMD` Layer**: The `CMD` instruction specifies the default command to run when a container is started from the image. It doesn't create a new layer but rather sets the metadata for the image. In this example, `CMD ["node", "index.js"]` sets the command to run the `index.js` file using Node.js.
6. **Layer Caching**: Docker caches layers to speed up subsequent builds. If a layer hasn't changed since the last build, Docker reuses the cached layer instead of rebuilding it. In the build logs, you can see `CACHED` next to the `WORKDIR` instruction, indicating that the layer was reused from the cache.

> By understanding how layers are created and utilized in Docker, you can optimize your Dockerfiles to minimize the number of layers and leverage caching effectively. This helps reduce build times and image sizes, making your Docker builds more efficient.
> 

## **Why layers?**

 Layers in Docker provide several benefits, including efficient caching and reusability. Let's explore why layers are important and how they can be optimized to maximize caching and minimize rebuild times.
### **Reusability and Caching**

One of the primary reasons for using layers in Docker is to enable reusability and caching. When you build a Docker image, each instruction in the Dockerfile creates a new layer. Docker caches these layers and reuses them in subsequent builds if the instructions and their inputs haven't changed.

### **Case 1 - Changing Source Code**

![s11.png](Docker%20b32a6be1c4274eff9bed8fcd0dc65e0c/s11.png)

Let's say you modify the `index.js` file and rebuild the image. Docker will reuse the cached layers for the base image, `WORKDIR`, `COPY package.json`, and `RUN npm install` instructions. Only the layer created by `COPY . .` will be rebuilt, as it includes the modified `index.js` file.

![s12.png](Docker%20b32a6be1c4274eff9bed8fcd0dc65e0c/s12.png)

### **Case 2 - Changing Dependencies**

![s13.png](Docker%20b32a6be1c4274eff9bed8fcd0dc65e0c/s13.png)

Now, let's consider a scenario where you modify the `package.json` file to add a new dependency. In this case, Docker will reuse the cached layers up to the `COPY package.json .` instruction. However, the `RUN npm install` layer and all subsequent layers will be rebuilt because the input to `npm install` has changed.

![s14.png](Docker%20b32a6be1c4274eff9bed8fcd0dc65e0c/s14.png)

</aside>

![https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fb14ff207-2687-41bc-9211-edd84fd25957%2FUntitled.png?table=block&id=aff2c522-1829-47e8-a7c3-13b35894baa0&cache=v2](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fb14ff207-2687-41bc-9211-edd84fd25957%2FUntitled.png?table=block&id=aff2c522-1829-47e8-a7c3-13b35894baa0&cache=v2)

![https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F366e9012-e174-40cc-8297-aa15ac5e1b29%2FUntitled.png?table=block&id=2f49b856-4d5f-4be7-9930-b9550d6c07cf&cache=v2](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F366e9012-e174-40cc-8297-aa15ac5e1b29%2FUntitled.png?table=block&id=2f49b856-4d5f-4be7-9930-b9550d6c07cf&cache=v2)

![https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fd7235b6f-08d9-462e-80fe-322807b69d34%2FUntitled.png?table=block&id=d8011ea0-1d92-46d7-900a-b3e2b4dc2a24&cache=v2](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fd7235b6f-08d9-462e-80fe-322807b69d34%2FUntitled.png?table=block&id=d8011ea0-1d92-46d7-900a-b3e2b4dc2a24&cache=v2)

![https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F89606a88-4a40-4192-a67d-0ddfc6429dab%2FUntitled.png?table=block&id=cd75c9e2-a54d-4fe5-8d1f-44fe3d2c1e30&cache=v2](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F89606a88-4a40-4192-a67d-0ddfc6429dab%2FUntitled.png?table=block&id=cd75c9e2-a54d-4fe5-8d1f-44fe3d2c1e30&cache=v2)

### **Thought Experiment**

In a typical project, dependencies (specified in `package.json`) change less frequently compared to the application code. By separating the `package.json` copy and `npm install` steps into their own layers, you can cache the `npm install` layer and avoid reinstalling dependencies every time the application code changes.

> This caching optimization becomes particularly valuable in larger projects with many dependencies. Reinstalling dependencies from scratch on every build can be time-consuming and resource-intensive. By leveraging caching, you can significantly speed up the build process and improve development efficiency.
> 

## **Optimising Dockerfile**

 To optimize your Dockerfile for caching, you should structure your layers in a way that maximizes the reuse of cached layers. Here are a few best practices:

1. Place instructions that are less likely to change at the top of the Dockerfile. For example, the base image and `WORKDIR` instructions are usually stable and can be cached effectively.
2. Separate the copying of `package.json` and the running of `npm install` into their own layers. This allows the `npm install` layer to be cached and reused as long as the `package.json` file remains unchanged.
3. Copy the application code (`COPY . .`) after installing dependencies. This ensures that changes to the application code don't invalidate the cached layers for installing dependencies.

By following these practices, you can optimize your Dockerfile to leverage caching effectively. This reduces build times and saves resources by reusing cached layers whenever possible.

What if we change the Dockerfile a bit -

```
FROM node:20

WORKDIR /usr/src/app

COPY package* .
COPY ./prisma .
    
RUN npm install
RUN npx prisma generate

COPY . .

RUN npm run build

EXPOSE 3000

CMD ["node", "dist/index.js", ]
```

1. We first copy over only the things that `npm install` and `npx prisma generate` need
2. Then we run these scripts
3. Then we copy over the rest of the source code

![https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F7cca333a-2fa4-4367-b730-e03cb85c6e41%2FUntitled.png?table=block&id=2f457b7a-316e-4329-9d30-90756e9d4306&cache=v2](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F7cca333a-2fa4-4367-b730-e03cb85c6e41%2FUntitled.png?table=block&id=2f457b7a-316e-4329-9d30-90756e9d4306&cache=v2)

[https://www.notion.so/image/https%3A%2F%2Fwww.notion.so%2Fimage%2Fhttps%253A%252F%252Fprod-files-secure.s3.us-west-2.amazonaws.com%252F085e8ad8-528e-47d7-8922-a23dc4016453%252F3dc112b6-bf1a-4d48-acd4-dcaac3ef594a%252FScreenshot_2024-03-10_at_2.24.00_PM.png%3Ftable%3Dblock%26id%3Dd3ab0f48-79e0-47c0-8370-5d9e18accb34%26cache%3Dv2?table=block&id=d5985f02-ba7a-4564-bf41-7bab0565c2b1&cache=v2](https://www.notion.so/image/https%3A%2F%2Fwww.notion.so%2Fimage%2Fhttps%253A%252F%252Fprod-files-secure.s3.us-west-2.amazonaws.com%252F085e8ad8-528e-47d7-8922-a23dc4016453%252F3dc112b6-bf1a-4d48-acd4-dcaac3ef594a%252FScreenshot_2024-03-10_at_2.24.00_PM.png%3Ftable%3Dblock%26id%3Dd3ab0f48-79e0-47c0-8370-5d9e18accb34%26cache%3Dv2?table=block&id=d5985f02-ba7a-4564-bf41-7bab0565c2b1&cache=v2)

### **Case 1 - You change your source code (but nothing in package.json/prisma)**

![s15.png](Docker%20b32a6be1c4274eff9bed8fcd0dc65e0c/s15.png)

![https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F9f5ab4f0-db0a-4cdb-80ce-28b2075dbcc1%2FUntitled.png?table=block&id=b26e63f7-96b6-4637-8302-81d68ca138c9&cache=v2](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F9f5ab4f0-db0a-4cdb-80ce-28b2075dbcc1%2FUntitled.png?table=block&id=b26e63f7-96b6-4637-8302-81d68ca138c9&cache=v2)

[https://www.notion.so/image/https%3A%2F%2Fwww.notion.so%2Fimage%2Fhttps%253A%252F%252Fprod-files-secure.s3.us-west-2.amazonaws.com%252F085e8ad8-528e-47d7-8922-a23dc4016453%252F60fd50e5-576a-4039-a0e0-6617293d10ce%252FScreenshot_2024-03-10_at_2.29.47_PM.png%3Ftable%3Dblock%26id%3De69f3527-8cd6-42a7-9d94-b17ac42467f0%26cache%3Dv2?table=block&id=459f2609-e55d-4c29-a6ca-27963e207230&cache=v2](https://www.notion.so/image/https%3A%2F%2Fwww.notion.so%2Fimage%2Fhttps%253A%252F%252Fprod-files-secure.s3.us-west-2.amazonaws.com%252F085e8ad8-528e-47d7-8922-a23dc4016453%252F60fd50e5-576a-4039-a0e0-6617293d10ce%252FScreenshot_2024-03-10_at_2.29.47_PM.png%3Ftable%3Dblock%26id%3De69f3527-8cd6-42a7-9d94-b17ac42467f0%26cache%3Dv2?table=block&id=459f2609-e55d-4c29-a6ca-27963e207230&cache=v2)

### **Case 2 - You change the package.json file (added a dependency)**

![s16.png](Docker%20b32a6be1c4274eff9bed8fcd0dc65e0c/s16.png)

[https://www.notion.so/image/https%3A%2F%2Fwww.notion.so%2Fimage%2Fhttps%253A%252F%252Fprod-files-secure.s3.us-west-2.amazonaws.com%252F085e8ad8-528e-47d7-8922-a23dc4016453%252Fda3357b0-33e6-47ab-b552-4e52ecbfa808%252FScreenshot_2024-03-10_at_2.30.51_PM.png%3Ftable%3Dblock%26id%3Dc8cc1aaf-8c6a-48d4-b764-f1531207260b%26cache%3Dv2?table=block&id=1889b790-cf0b-4c43-a5f6-f85a4af47121&cache=v2](https://www.notion.so/image/https%3A%2F%2Fwww.notion.so%2Fimage%2Fhttps%253A%252F%252Fprod-files-secure.s3.us-west-2.amazonaws.com%252F085e8ad8-528e-47d7-8922-a23dc4016453%252Fda3357b0-33e6-47ab-b552-4e52ecbfa808%252FScreenshot_2024-03-10_at_2.30.51_PM.png%3Ftable%3Dblock%26id%3Dc8cc1aaf-8c6a-48d4-b764-f1531207260b%26cache%3Dv2?table=block&id=1889b790-cf0b-4c43-a5f6-f85a4af47121&cache=v2)

![https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F6ca4a715-a648-4799-8734-e1da9500f3d5%2FUntitled.png?table=block&id=257edec1-4e62-401e-b1f4-731be7444d3a&cache=v2](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F6ca4a715-a648-4799-8734-e1da9500f3d5%2FUntitled.png?table=block&id=257edec1-4e62-401e-b1f4-731be7444d3a&cache=v2)

In Docker, layers are a fundamental part of the image architecture. A Docker image is essentially built up from a series of layers, each representing a set of differences from the previous layer. These layers are stacked on top of each other, forming the complete image.
