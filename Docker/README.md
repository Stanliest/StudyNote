[cognitiveClass.ai](cognitiveClass.ai) - Docker Essentials: A Developer Introduction
[Docker Docs](https://docs.docker.com/)
# Docker Essentials

## Containers
Containers are processes running in isolation, achieved with Linux namespaces and control groups. Isolation benefits are possible because of Linux namespaces.
* control groups(cgroups): limit an application to specific set of resources

### Run a container
1. run container:\
`docker container run -t ubuntu top`
    1. Using the ubuntu image, which provide the file system and tools available on ubuntu system
    2. Container **does not** have its own kernal, it's using the kernal of the host

2. get id of running containers:\
`docker container ls` (in a separate terminal)

3. inspect the container:\
`docker container exec -it [container id] bash`
    1. enter the running container's namespace with a new process
    2. -it: run using interactive mode

4. inspect the running process:  
`ps -ef`

5. clean up the container running the processes:  
`<ctrl>-c`

### Run multiple containers
Run an NGINX server:\
`docker container run --detach --publish 8080:80 --name nginx nginx`
* --detach: run container in the background  
* --publish: publishes port 80 in container using port 8080 on your host, this flag is a feature that can expose networking through the container onto the host. Why 80? It's the default port for NGINX in official doc in docker store.
* --name: names the container   

Run mongo database:\
`docker container run --detach --publish 8081:27017 --name mongo mongo:3.4`

### Remove the containers
1. Stop containers:\
`docker container stop [container id]`
2. Remove stopped containers: (remove dangling images, containers, volumes, and networks)\
`docker system prune`

## Docker Images
1. *Dockerfile*
```
FROM python:3.6.1-alpine
RUN pip install flask
CMD ["python","app.py"]
COPY app.py /app.py
```
**FROM python:3.6.1-alpine**
This is the base layer. If no tag '3.6.1-alpine' is specified, it will pull the latest versiion of the image.

**RUN pip install flask**
RUN execute command needed to set up your image for the application. RUN executes at build time.

**CMD ["python","app.py"]**
CMD is the command to use when start a container. There can be only one CMD for per Dockerfile.

**COPY app.py /app.py**
This line copies the app.py file in the local directory (where you will run docker image build) into a new layer of the image. Layers that change frequently, such as copying source code into the image, should be placed near the bottom of the file to take full advantage of the Docker layer cache

[Dockerfile Reference](https://docs.docker.com/engine/reference/builder/)

2. Build the docker image\
`docker image build -t python-hello-world .`\
Adding a tag to the image:\
`docker image build -t python-hello-world:latest .`

3. Run the docker image\
`docker run -p 5001:5000 -d python-hello-world`
    1. **-p**: maps the Python app running on port 5000 inside the container to port 5001 on the host.

4. Push to central registry
```
docker login
docker tag python-hello-world [username]/python-hello-world
docker push [username]/python-hello-world
```
5. Deploy a change
-> changes to your app...
```
docker image build -t [username]/python-hello-world .
docker push [username]/python-hello-world
```
**Note**: if the change is very small, docker might cache the change when deploying through the same image. Need to rebuild the docker image with a different name.

## Container orchestration
1. Create swarm\
`docker swarm init --advertise-addr eth0`\
`docker node ls`

2. Deploy service\
A service is an abstraction that represents multiple containers of the same image deployed across a distributed cluster.\
i. Deploy a service by using NGINX:\
`docker service create --detach=true --name nginx1 --publish 80:80  --mount source=/etc/hostname,target=/usr/share/nginx/html/index.html,type=bind,ro nginx:1.12
pgqdxr41dpy8qwkn6qm7vke0q`\
* --mount: to have NGINX print out the hostname of the node it's running on
* --publish: uses the swarm's built-in routing mesh. In this case, port 80 is exposed on every node in the swarm

3. Inspect the serice\
`docker service ls`

4. 
