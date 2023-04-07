# Docker Crash Course For Absolute Beginners

https://www.youtube.com/watch?v=pg19Z8LL06w



## 1. What is Docker?

- **What?**
  - Virtualization software
  - Make developing and deploying applications easier
  - Packages app with all the dependencies, configuration, system tools, and runtime
- **Why?**
  - Each dev needs to install and configure all service directly on their OS on their local machine
  - There are many steps to install and configure
  - With containers you have services packages in one environment inside of the container
  - Docker standardizes process of running any service on any local dev environment
  - Easy to run different versions of the same app without any conflicts



## 2. Virtual Machine vs Docker

- Docker images are much smaller
- Docker images usually take seconds to start
- Docker is compatible only with Linux distros
- Docker developed Docker Desktop that enables Linux-based container on Windows an Mac
  - This uses Hypervisor layer with a lightweight Linux distro
- They only virtualize the application layer



## 3. Install Docker

- refer to latest installation guide online for **Docker Desktop** 
- Parts
  - **Docker Engine**
  - **Docker CLI-Client**
    - You can execute docker commands on CLI
  - **GUI Client**



## 4. Docker Images vs Docker Containers

- **image**
  - can be easily shared and moved
  - like a zip or tarfile
  - An executable application artifact
    - includes app source code and complete environment configuration
    - includes environment variables, directories, files, etc.
- **Container**
  - A running instance of an image
  - Actually starts the application
  - From one image you can run multiple containers



## 5. Docker Registries

- a storage for Docker images
- official images available from applications like Redis, Mongo, Postrgres, etc.
- **Docker Hub**  - www.hub-docker.com



## 6. Docker Image Versioning

- Docker images are versioned
- all images have special **latest** tag referring to the latest release



## 7. Main Commands

- viz. **CLI**
- you can run images you do not have locally



## 8. Port Binding

- applications inside container run in an isolated Docker network
- We need to expose the container to the host if we want to access it first.
- Usually choose the same port the container is using.

## 9. Start and Stop containers

- it always creates a new container
- it doesn't reuse the containers it created

## 10. Private docker Registries

- You can store them on **Docker Hub**.

## 11. Registry vs Repository

- Registry 
  - is a service providing storage
  - collection of repositories
- Repository
  - collection of related images with the same name but different versions



## 12. Dockerfile - Dockerize Node.js app

- we need to create a definition about how to build an image

- in the root of the app create **Dockerfile**

  - write the definition of the image
  - Dockerfile start from a parent or a base image - an image your docker is based on

- ```dockerfile
  FROM node:19-alpine
  
  # take the files from the local computer here into the /app/ folder
  # the slash at the end creates the folder if it doesnt exist yet
  COPY package.json /app/
  COPY src/app/
  
  # like cd
  WORKDIR /app
  
  RUN npm install
  
  # last command starts the application
  CMD ["node", "server.js"]
  ```



## 13. Creating docker image

```bash
docker build --tag node-app:1.0 .
```



# CLI

```bash
# List Running containers
docker ps

# List all the containers (even the stopped ones)
docker ps -a

# List local images
docker images

# Download specific image:tag
docker pull nginx:1.23

# Download latest image
docker pull nginx

# Run an image
docker run nginx:1.23

# Run an image detached from a terminal
docker run -d nginx:1.23

# show logs from detached image
docker logs [container_id || container_name]

# stop container
docker stop [container_id]

# To publish the container to the host
# This exposes the container to the port 9000
docker run -d -p 9000:80 nginx:1.23 

# Start docker with custom name
docker run --name web-app -d nginx:1.23
```



