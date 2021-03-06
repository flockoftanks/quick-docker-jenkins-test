# Commands for creating local Blue Ocan instance
### Create network
```bash
docker network create jenkins
```
### Create Volumes
```bash
docker volume create jenkins-docker-certs
docker volume create jenkins-data
```
### Run dind
```bash
docker container run --name jenkins-docker --rm --detach ^
  --privileged --network jenkins --network-alias docker ^
  --env DOCKER_TLS_CERTDIR=/certs ^
  --volume jenkins-docker-certs:/certs/client ^
  --volume jenkins-data:/var/jenkins_home ^
  docker:dind
```
### Run Blue Ocean
```bash
  docker container run --name jenkins-blueocean --rm --detach ^
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 ^
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 ^
  --volume jenkins-data:/var/jenkins_home ^
  --volume jenkins-docker-certs:/certs/client:ro ^
  --publish 8085:8080 --publish 50000:50000 jenkinsci/blueocean
```