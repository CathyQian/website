---
layout: post
title: Docker Tutorial
date: 2019-02-01
---

# Why use Docker?

One thing we probably do on a daily basis as a data scientist or software engineer is probably clone a repository, install a bunch of software it depends on and try to run it in our own machine. The problem is very often we get into endless cycle of running into installation errors and trouble shooting. When you move the repository to a new environment, you have to reinstall the software again.

The goal of Docker is to make it easy to install and run software without having to go through a whole bunch of setup or installation of dependencies.

# What is Docker?

Docker is a platform or ecosystem around creating and running containers. The Docker ecosystem contains Docker Client, Docker Server, Docker Machine, Docker Images, Docker Hub and Docker Compose.

An image is a single file containing all the dependencies and all the configuration required to run a very specific program. It gets stored on your hard drive and you can use it to create containers.

A container is an instance of an image and a program with its own isolated set of hardware resources.

Docker Client (Docker CLI): Tool that we are going to issue commands to. We will interact with it directly.

Docker Server (Docker Server): Tool that is responsible for creating images, running containers, etc. It's running behind the scenes and we never interact with it directly.

# How to install Docker?
First, register for a Docker Hub account [here](https://hub.docker.com/). Then download Docker Desktop (Windows) from Docker Hub [here](https://hub.docker.com/editions/community/docker-ce-desktop-windows). Start Docker Desktop before using it.

# How to use Docker?

Assume I have built an web-based app. The front-end is written in HTML and CSS, and the back-end is mostly in Python and Flask. I've run the app successfully in my local server in my Windows 10 machine, and now I want to use Docker to wrap it so that I can use it anywhere in any machine.

Let's say my current file directory (let's name it root directory) looks like the following:

**Name** -------------------- **Type**

static --------------------- File folder

templates ---------------- File folder

app.py -------------------- Python File

requirements.txt --------- Text Documents

README.MD ------------- MD File

Here the _static_ folder contains mutilple subfolders all related to the UI design of the web-based app. The _templates_ folder contains html pages the web-based app is made of. _app.py_ is key file to run the app. _requirements.txt_ includes a list of software needs to be installed to run the app (you don't need to include python here since it will be installed in _Dockerfile_, see below). The _README.MD_ file includes detailed instructions about this app and how to run it.

First, create _Dockerfile_ under the root directory. It defines what goes on in the environment inside your container. Copy-and-paste the following content into that file, and save it.

```
# Use an official Python runtime as a parent image
# Here the Python version needs to be the one needed to run your existing app
FROM python:3.5-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 80 available to the world outside this container
# Without this line, your app won't be able to run using Docker container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

Next, open a Windows PowerShell or Anaconda Prompt. Check your docker version to make sure it is running on your machine using the following command:

```
$ docker -v
```

Then log into your Docker Hub so that you can push and pull images later using the following command:

```
$ docker login
```
If you don't have a Docker account, go to https://hub.docker.com to create one. Without successful login, you won't be able to proceed to the next step.

Let's first check existing Docker images and containers:

```
$ docker image ls
```

```
$ docker container ls --all
```

All the above command line can be run in any directory. Now let's go to the root directory mentioned above and start to use Docker for our web-based app.

First, build a Docker image for the app using the following command line under the root directory:

```
$ docker build --tag=studentgrade:v1
```
or 
```
$ docker build --tag=studentgrade .
```
Here studentgrade is my Docker image name, v1 is additional note denoting version 1. If everything goes well, all packages in the requirements.txt file will be installed and a Docker image will be successfully created. The whole process may take a while and you will see the progress in the command line.

If you check the Docker image list again, you will see the newly added image, like the following:

**REPOSITORY** --- **TAG** --- **IMAGE ID** --------- **CREATED** ---------- **SIZE**

studentgrade --- v1 ---- 5b25835bbad6 --- 22 seconds ago --- 423MB

Next, run the app and map your machine’s port 5000 (or other numbers depending on the machine's local port) to the container’s published port 80 using the following command:

```
$ docker run -p 5000:80 studentgrade:v1
```

The command line will show "Running on http://x.x.x.x:80/" (here the x.x.x.x comes from app.run(host = 'x.x.x.x', port=80) in your app.py file) Change 80 to 5000 and copy-and-paste the http into your browser. Your app should be running now.

Now you probably want to share your image so that you can run it in any machine. Let's upload our built image and run it somewhere else. Login to Docker Hub using

```
$ docker login
```

Then tap the image using the following command:

```
$ docker tag studentgrade myusername/studentgrade:v1
```

After finishing this step, run 

```
$ docker image ls
```

You will see your newly tagged image as follows:

**REPOSITORY** ------------------ **TAG** --- **IMAGE ID** --------- **CREATED** ---------- **SIZE**

myusername/studentgrade --- v1 ---- xxxxxxx ------------ 10 seconds ago --- 423MB

Then upload your tagged image to the Docker Hub repository:

```
$ docker push myusername/studentgrade:v1
```

Once complete, the uploaded image will be publicly available. You will see it if you log in to Docker Hub along with the instructions on how to pull and run in your own machine.

# How to save Docker image locally and use in another machine?
Sometimes, we don't want to push Docker images to either public or private repositories due to privacy reasons. Instead, we need to save Docker images locally, transfer into another machine like a regular file and reuse. 
Save the Docker image as a tar file locally:
```
docker save -o <path for generated tar file> <image name>
```
For example,
```
docker save -o dockerimage.tar studentgrade:v1
```

Then you can copy your .tar file to a new system and load the image into Docker as such:
```
docker load -i <path for generated tar file>
```
For example, 
```
docker load -i dockerimage.tar
```

References:

1, https://medium.com/coinmonks/docker-in-a-nutshell-6b3985a58d68

2, https://docs.docker.com/get-started/part2/
