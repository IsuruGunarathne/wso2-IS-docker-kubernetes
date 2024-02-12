# Deploying an IS 7.0 docker image

## Deploying on docker

Copy the IS 7.0 folder (named wso2is-7.0.0) to the docker folder and run the following commands

#### start docker

`sudo systemctl start docker`

#### Build image

`docker build -t is7.0 .` image will be named IS7.0

#### Delete docker image

`docker rmi is7.0` delete image named IS7.0
`docker rmi -f is7.0` force delete image named IS7.0`

#### Run container

`docker run -d --rm -p 127.0.0.1:9443:9443 is7.0` run container in background and map port 8080 to 8080

#### view all containers

`docker ps -a`

#### logs for the container

`docker logs -f <container id>`

#### Stop container

`docker stop <container id>`

#### remove all containers

`docker container prune`

#### checking the container

`docker exec -it <container id> /bin/bash` <br>

## Deploying on kubernetes (using minikube)

#### start minikube

`minikube start` <br>
kubectl is required for steps to follow<br>
run `alias kubectl="minikube kubectl --"` to use minikube kubectl<br>
OR <br>
`sudo snap install kubectl --classic` to install kubectl

#### get the image from docker repository or build from within minikube

`eval $(minikube docker-env)`

#### Build image again and check local mini kube repository

`docker build -t is7.0 .` image will be named IS7.0 <br>
OR <br>
`minikube image load is7.0` load image to local mini kube repository from docker repository <br>
`minikube image ls` check local mini kube repository

#### deploy IS 7.0

`kubectl create -f is.yaml`

#### view logs to confirm deployment

get pod name using `kubectl get pods`
`kubectl logs -f <pod name>`

#### expose IS 7.0 deployment (optional)

This exposes the deployment directly to the host machine and creates a service named with the same name as the deployment

`kubectl expose deployment is-deployment --type=NodePort --port=9443 --target-port=9443`

#### view all deployments

`minikube service is-deployment --url` change link to https:// to access IS 7.0 deployment on kubernetes <br>
or <br>
`minikube service is-service --url` change link to https:// to access IS 7.0 deployment on kubernetes

#### list all services on minikube

`minikube service list`

#### view all services

`kubectl get services`

#### delete cluster

`minikube delete --all`
