# docker-udemy-microservices
Some notes about the basics of Docker, took them from the UDEMY course Microservices with Java

# Docker Architecture
![image](https://user-images.githubusercontent.com/36638342/143726548-47060a9f-3aaf-4331-b5c8-a76a0a7f1170.png)


# Installation
For Windows: Execute the installer, restart and that's it.

# Basic Concepts
- Default Registry https://hub.docker.com/ where Docker images are stored. (Docker Hub)
- Docker Registry contains a number of repositories, "in28min/todo-rest-api-h2" is the name of the repo
- ":1.0.0.RELEASE" Which version, Which tag of that repository we want.
- The image pulled from Docker Hub is only that, an image.
- The running version of an Docker image is called a container, "For the same image, you can run multiple containers"



# Basic Commands used in the videos of the course
``docker --version`` --> Display in your terminal the version of Docker

``docker run in28min/todo-rest-api-h2:1.0.0.RELEASE`` --> Download the image and run the Container with a basic App with Java 8, Tomcat, 
If you go in your brwser to https://hub.docker.com/r/in28min/todo-rest-api-h2, you can see the content of the image


https://hub.docker.com --> Public repository of Docker images

 Image --> Static
 
 Container --> Image Running

"For the same image, you can run multiple containers"

# To Expose a docker container in a local port
``docker run -p 5000:5000 in28min/todo-rest-api-h2:1.0.0.RELEASE``  -->  -p {HostPort}:{ContainerPort}

In this way the container that is running the app in his port 5000 connects with the port 5000 of my machine and let me do ``http://localhost:5000/hello-world-bean``

# Run a container in the background
To not attach the lifecycle of the container to the terminal, we can add ``-d`` to the options when we are running the container

``docker run -p 5000:5000 -d in28min/todo-rest-api-h2:1.0.0.RELEASE``

You will get an ID but you will get free the prompt in the terminal, the conotainer is running in the backgorund.
![image](https://user-images.githubusercontent.com/36638342/143725999-97f6ca8a-392a-4ce5-a4ec-db27e0557ab9.png)

# You can check the logs of that container with:
``docker logs 09c37b66517d8841bf26129b42b0543babbbdc4081153ba1da89983d13db4bca`` --> Display logs of the image
``docker logs -f 09c37b66517d8841bf26129b42b0543babbbdc4081153ba1da89983d13db4bca`` --> Display logs of the image but doesn't stop

# Which Docker containers are running right now 
``docker container ps `` or ``docker container ls `` or ``docker container ls -a ``  
![image](https://user-images.githubusercontent.com/36638342/143726163-375504cb-d0cf-4ce7-b987-38f1fd46d012.png)

- The first two display the current containers  running
- The third one displays all the container, including the stoped ones.

# Running another container of the same image
e.g Run two containers, both exposed in Host Ports, one using the port 5000 and the other one the 5001

``docker run -p 5000:5000 -d in28min/todo-rest-api-h2:1.0.0.RELEASE ``
``docker run -p 5001:5000 -d in28min/todo-rest-api-h2:1.0.0.RELEASE ``

# Display the Docker images pulled rom Docker Hub that are in your local 
``docker images``
![image](https://user-images.githubusercontent.com/36638342/143726178-dd585958-2d90-4561-ba25-19e20258642e.png)

# How to stop a Docker container
- Use the 5 first digits of the container listed using ``docker container ls``

![image](https://user-images.githubusercontent.com/36638342/143726198-3ba731ad-81be-4e58-825d-d7937b714c5c.png)



