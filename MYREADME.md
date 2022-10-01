## docker_fundamentals
* docker self-study project
* [docker zero to hero](https://www.youtube.com/watch?v=3c-iBn73dDE)
  * about 3 hr
* docker images
* docker ps
* docker ps -a
  * all the container including stoped ones
* docker build
  * create a docker image
* docker run
  * create a docker container based on an image
* docker start
  * run a stoped container
* docker network *network_name*
  * multiple docker containers need to be on the same docker network to talk to each other
  * ex: docker container for web application, docker container for mongo db, docker container for mongo express
* docker logs *container_id* | tail
* docker compose
  * A tool for automating to run multiple containers
  * use a .yaml file
  
