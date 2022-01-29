---
created: 17.10.2021
tags: docker
---

# Setup docker in docker

[Example for jenkins](https://www.jenkins.io/doc/tutorials/create-a-pipeline-in-blue-ocean/)

[Description on dockerhub](https://hub.docker.com/_/docker?tab=description)

```bash

docker container run --name jenkins-docker --rm --detach \
  --privileged --network jenkins --network-alias docker \
  --env DOCKER_TLS_CERTDIR=/certs \
  --volume jenkins-docker-certs:/certs/client \
  --volume jenkins-data:/var/jenkins_home \
  --volume "$HOME":/home docker:dind
  
  
 docker container run --name jenkins-tutorial --rm --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  --volume "$HOME":/home --publish 8080:8080 jenkinsci/blueocean

  ```

  ```yaml
  version: '2.0'
services:
  docker:
    privileged: yes
    environment:
      DOCKER_TLS_CERTDIR: "/certs"    
    volumes:
      - docker-data:/var/lib/docker
      - certs:/certs/client
    image: docker:dind
  docker-client:
    environment:
      DOCKER_HOST: tcp://ADD_IP_HERE:2376
      DOCKER_CERT_PATH: "/certs/client"
      DOCKER_TLS_VERIFY: 1
    volumes:
      - certs:/certs/client:ro
    image: jenkinsci/blueocean
volumes:
  docker-data:
  certs:  
  ```
