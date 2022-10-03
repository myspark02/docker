## docker_fundamentals
* docker self-study project
* [Youtube content: docker zero to hero](https://www.youtube.com/watch?v=3c-iBn73dDE)
  * about 3 hr
* [Reference source code](https://gitlab.com/nanuchi/techworld-js-docker-demo-app)
* docker images
* docker ps
* docker ps -a
  * all the container including stoped ones
* docker build
  * create a docker image
* docker run
  * create a docker container based on an image
* docker exec -it *docker_image_id* /bin/bash
  * get a interactive terminal to execute commands from the container
* docker start
  * run a stoped container
* docker network *network_name*
  * multiple docker containers need to be on the same docker network to talk to each other
  * ex: docker container for web application, docker container for mongo db, docker container for mongo express
* docker logs *container_id* | tail
* docker compose
  * A tool for automating to run multiple containers
  * Docker Compose takes care of creating a common network
    * So we don't have to create the network and specify in which network these containers will run in.
  * use a .yaml file
  * <img src="https://github.com/myspark02/docker/blob/main/MappingDockerRun2YAML.png?raw=true" alt="docker run mapping">
  * docker-compose command
    * Already installed as a docker package
    * docker-compose -f *docker_compose_file.yaml* up -d
      * starts all the containser in the yaml file
    * docker-compose -f *docker_compose_file.yaml* down
      * removes all the containers as well as the docker network created based on the yaml file
    * docker network ls
* Dockerfile
  * Pull Mongo DB from docker hub → Developing a Javascript App → Commit to Git → Jenkins
  * Jenkins
    * Build JS App & creates Docker Imagev → Push to Docker Repository
  * Docker file is blueprint for building images
  * Syntax for Docker file is super simple
  * Starts by basing it on another image
  * Syntax
    * FROM
      * pull a docker image
    * ENV
      * sets an environmental variable
    * RUN
      * executes any linux comand
      * ex: 
        * RUN mkdir -p /home/app
          * directory is created INSIDE of the container!
    * COPY
      * executes on the HOST machine!
    * CMD
      * Entrypoint command
      * The difference between RUN and CMD is the CMD is entrypoint command
      * ex:
        * CMD ["node", "server.js"]
          * → node server.js
    * docker build -t *image_name_to_build:tag* *folder_the_image_will_be_located*
      * ex :
        * docker build -t my_app:1.0 .
* docker rm *container_id_or_name*
* docker rmi *image_id_or_name*
  * deletes a docker image
  * must delete containers created from this image first
* private docker registry
  * Create private docker registry on AWS
    * ECR (Elastic Container Registry)
      * Repository per image 
  * push a local image to the registry
    * 1. log into the private repository
      * docker login
        * need to reference document for Amazone ECR 
    * 2. push local docker image to the registry. 
      * to push to private docker registry you need an image appropriatly named. 
      * reference the below about image naming
  * Image Naming in docker registries.
    * registryDomain/imageName:tag
  * In docker hub
    * docker pull mongo:4.2
      * is equivalent to the below
      * docker pulll docker.io/library/mongo:4.2
  * In AWS ECR
    * We can't use shorthand pull syntax like in docker hub
    * docker pull 520697001743.dkr.ecr.eu-central-1.amazonaws.com/my-app:1.0
* docker tag
  * renaming name of an image
  * docker tag *source_image_name* *target_image_name*
  * ex :
    * docker tag my-app:latest 520697001743.dkr.ecr.eu-central-1.amazonaws.com/my-app:1.0
* push to private docker registry
  * ex:
    * AWS
    * docker push 520697001743.dkr.ecr.eu-central-1.amazonaws.com/my-app:1.0
      * parameter of docker push is information about the image to push 
        * registry domain
        * image name
        * tag (version)
* deploy containerized app
  * contents
    * image from private repository
    * deploy multiple containers
    * deployment server
  * The server needs to login to pull from PRIVATE repository
  * Login not needed for PUBLIC DockerHub
  * This Docker Compose file would be used on the server to deploy all the applications/services
* Docker Volumes
  * Overview
    * When do we need Docker Volumes?
    * What is Docker Volumes?
    * 3 Volume Types
    * Docker Volumes in docker-compose file
  * Docker Volumes are used for data persistence in docker
  * data in virtual file system is gone! when restarting or removing he container
  * Folder in physical host file system is **mounted** into the virtual file system of Docker.
  * 3 Volue Types
    * Host Volumes
      * you decide where on the host file system the reference is made
      * docker run
        * -v /home/mount/data:/var/lib/mysql/data
    * Anonymous Volumes
      * for each container a folder is generated that gets mounted
      * docker run
        * -v /var/lib/mysql/data
    * Named Volumes
      * you can reference the volume **by name**
      * should be used in production
      * docker run 
        * -v name:/var/lib/mysql/data
  * Docker Volumes in docker-compose
  * Docker Volums Locations
