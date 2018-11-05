cognitiveClass.ai - Docker Essentials: A Developer Introduction
# Docker Essentials

## Containers
Containers are processes running in isolation, achieved with Linux namespaces and control groups

### Run a container
1. run container: `docker container run -t ubuntu top`
  1. Using the ubuntu image, which provide the file system and tools available on ubuntu system
  2. Container **does not** have its own kernal, it's using the kernal of the host

2. get id of running containers: `docker container ls` (in a separate terminal)

3. inspect the container: `docker container exec -it <container id> bash`
  1. enter the running container's namespace with a new process
  2. -it: run using interactive mode

4. inspect the running process: `ps -ef`

5. clean up the container running the processes: `<ctrl>-c`

### Run multiple containers
