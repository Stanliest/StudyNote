cognitiveClass.ai - Docker Essentials: A Developer Introduction
# Docker Essentials

## Containers
Containers are processes running in isolation, achieved with Linux namespaces and control groups. Isolation benefits are possible because of Linux namespaces.

### Run a container
1. run container:
* `docker container run -t ubuntu top`
    1. Using the ubuntu image, which provide the file system and tools available on ubuntu system
    2. Container **does not** have its own kernal, it's using the kernal of the host

2. get id of running containers:
* `docker container ls` (in a separate terminal)

3. inspect the container:
* `docker container exec -it [container id] bash`
    1. enter the running container's namespace with a new process
    2. -it: run using interactive mode

4. inspect the running process:
* `ps -ef`

5. clean up the container running the processes:
* `<ctrl>-c`

### Run multiple containers
Run an NGINX server:
* `docker container run --detach --publish 8080:80 --name nginx nginx`
    1. --detach: run container in the background
    2. --publish: publishes port 80 in container using port 8080 on your host, this flag is a feature that can expose networking through the container onto the host
    3. --name: names the container

### Remove the containers
1. Stop containers:
* `docker container stop [container id]`
2. Remove stopped containers:
* `docker system prune`
