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

 Image --> Static![143726816-09055e9b-d2f1-43cd-a446-355485693a84](https://user-images.githubusercontent.com/36638342/143726916-7695031b-26b0-4e54-9684-c9ccd5a6c45f.png)

 
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

# Docker IMAGES commands

# Add another TAG to an existing Docker image
``docker tag  in28min/todo-rest-api-h2:1.0.0.RELEASE in28min/todo-rest-api-h2:latest`` -- This add the "latest" tag

- In Docker Hub, some of the images containg "latest" as the tag for the most recent version, BUT THIS DOEN'T HAPPEN THE WHOLE TIME, you need to review the version you need.
  - e.g ``docker pull mysql`` by default Docker will pull the image with the "latest" tag on it.
  - ![image](https://user-images.githubusercontent.com/36638342/143726734-09323ab8-67ba-4e08-a2e2-f33191cc21e2.png)

# Check the history of an image
``docker image history  b05128b000dd`` --> docker image history {IMAGE ID}

![image](https://user-images.githubusercontent.com/36638342/143726816-09055e9b-d2f1-43cd-a446-355485693a84.png)

# Inspect an specific image
``docker image inspect b05128b000dd`` --> docker inspect imafe {IMAGE ID }
- All the details of the images (Configurations and structure)
- 
![image](https://user-images.githubusercontent.com/36638342/143726911-0e276437-588f-4114-9220-c889eb385ac3.png)


# Docker CONTAINERS commands

# Pause and run a Docker Container

``docker container pause 49f9`` --> docker container pause {first 4 digists of ID}

![image](https://user-images.githubusercontent.com/36638342/143727062-163b023c-f60c-4d2d-b7b7-03583bb5c24b.png)

 - The container is still running, but if you want to send a request it won't respond.

``docker container unpause 49f9`` --> docker container unpause {first 4 digists of ID}
 - The container continue running


# Inspect a container
``docker container inspect 49f9`` --> docker container unpause {first 4 digists of ID}

![image](https://user-images.githubusercontent.com/36638342/143727128-b7c2a025-825d-44a3-b970-bd09afbbefdf.png)

- All the details if that container, the state, configurations, ports.


# Display Docker containers that are running or were stopped 
``docker container ls a`` 

- Status of the latest containers, which ones are running, which ones were stopped.
![image](https://user-images.githubusercontent.com/36638342/143727160-2fe5151f-04fa-4dc0-bd75-68503de9075f.png)


#  Remove all the containers stopped
``docker container prune``

![image](https://user-images.githubusercontent.com/36638342/143727197-35d4e19c-1cd4-414f-a066-6d49cb40eb7c.png)

# Stop a Docker container
``docker container stop 49f9`` --> docker container stop {CONTAINER ID}

- Stops the Container in a graceful way [SIGTERM]


``docker container kill 49f9`` --> docker container stop {CONTAINER ID}

- Stops the Container terminating the process at that moment [SIGKILL]

# Restart policy of a Docker Container
`` docker run -p 5000:5000 -d --restart=always in28min/todo-rest-api-h2:1.0.0.RELEASE ``
- Restarts automatically a Docker container when the Docker Desktop is restarted
- The default value is "no" 

![image](https://user-images.githubusercontent.com/36638342/143727366-9f43d71b-e51f-48d8-a613-641f130b5eed.png)

** Could help for the DB images like MySQL, PostgreSQL, etc


#  Other Docker commands 

# Docker events logs
``docker events`` --> log of Docker, if yo trigger a Docker command in other tab the log information will be placed here

![image](https://user-images.githubusercontent.com/36638342/143727454-5951fe86-d202-48c8-b86a-66b1ca4a3f55.png)


# Display the main command of specifi container
``docker container top 8e1cf2e0608b`` -->  docker container top {CONTAINER ID}
- Displays the top command executed in the container 
- ![image](https://user-images.githubusercontent.com/36638342/143727493-a3f4c7b7-6955-4812-9187-956178c53456.png)

# Display statistics like requests, memory, CPU usage 
``docker stats``

![image](https://user-images.githubusercontent.com/36638342/143727541-7b95838e-f57e-4cb4-a508-e82bba6ad14c.png)

# Assigning limit of Memory RAM and CPU to a container
``docker run -p 5001:5000 -d -m 512m --cpu-quota 5000 in28min/todo-rest-api-h2:1.0.0.RELEASE`` --> docker run -p 5001:5000 -d -m {memory in Megabytes or Gigabytes} --cpu-quota {CPU Percentage, quantity divided by 1000}  in28min/todo-rest-api-h2:1.0.0.RELEASE

![image](https://user-images.githubusercontent.com/36638342/143727615-88befcab-446f-4383-850f-3040f22630cb.png)

Statistics (Check CPU and MEM USAGE)
![image](https://user-images.githubusercontent.com/36638342/143727621-dac6d6cf-b8e7-4a2a-8b00-3f5c02413186.png)

# General status of your Docker
``docker system df``

![image](https://user-images.githubusercontent.com/36638342/143727683-a0012771-04dc-4bea-825d-e32bb6383da7.png)

