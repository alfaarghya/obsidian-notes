![s1.png](Docker%20b32a6be1c4274eff9bed8fcd0dc65e0c/s1.png)

---

## Let's understand Docker
Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker's methodologies for shipping, testing, and deploying code, you can significantly reduce the delay between writing code and running it in production.
### [[Why Docker ??]]

---
## **Containerization**
 Containerization is a technology that allows you to package and distribute software applications in a consistent and isolated manner, making it easier to deploy and run them across different environments. Let's elaborate on the points you've provided:
### [[Deep Drive Containerization]]

---
## **Installing Docker**

 Docker provides official installation instructions for various operating systems, including Windows, macOS, and different Linux distributions. You can find the installation guide for your specific operating system on the official Docker documentation website: [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/)

### [[Install Docker]]

---

## **Images vs containers**

The main difference between a Docker image and a Docker container is that images are static and read-only, while containers are dynamic and can be modified.
### [[Image vs Container]]

---

## **Docker commands**
This _command_ is used to run a container from an image. The _docker_ run _command_ is a combination of the _docker_ create and _docker_ start _commands_.
### [[CLI Command]]

---
## **Dockerfile**
A Dockerfile is a text document that contains a set of instructions for building a Docker image. It specifies the base image to start from and the steps required to create the desired environment for your application, such as installing dependencies, copying files, and setting environment variables.
### [[Dockerfile]] 

---

## **Layers In Docker**

 In Docker, layers are a fundamental part of the image architecture. A Docker image is essentially built up from a series of layers, each representing a set of differences from the previous layer. These layers are stacked on top of each other, forming the complete image.
### [[Layers Deep Drive]]

---

## **Networks and volumes**

 Networks and volumes are essential concepts in Docker that enable communication between containers and data persistence across container restarts. Let's explore these concepts in more detail.

### [[Network & volumes]]

---
## [[Docker compose]]

