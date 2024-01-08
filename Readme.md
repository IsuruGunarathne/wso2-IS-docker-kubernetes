# Deploying and IS 6.1 docker image

## Deploying on docker

Copy the IS 6.1 folder (named wso2is-6.1.0) to the docker folder and run the following commands

#### start docker

`sudo systemctl start docker`

#### Build image

`docker build -t is6.1 .` image will be named IS6.1

#### Delete docker image

`docker rmi is6.1` delete image named IS6.1
`docker rmi -f is6.1` force delete image named IS6.1`

#### Run container

`docker run -d --rm -p 127.0.0.1:9443:9443 is6.1` run container in background and map port 8080 to 8080

#### view all containers

`docker ps -a`

#### logs for the container

`docker logs -f <container id>`

#### Stop container

`docker stop <container id>`

#### remove all containers

`docker container prune`

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

`docker build -t is6.1 .` image will be named IS6.1 <br>
OR <br>
`minikube image load is6.1` load image to local mini kube repository from docker repository
`minikube image ls` check local mini kube repository

#### deploy IS 6.1

`kubectl create -f is.yaml`

#### view logs to confirm deployment

get pod name using `kubectl get pods`
`kubectl logs -f <pod name>`

#### expose IS 6.1 port

`kubectl expose deployment is-deployment --type=NodePort --port=9443 --target-port=9443`

#### view all deployments

`minikube service is-deployment --url` change link to https:// to access IS 6.1 deployment on kubernetes
or
`minikube service is-service --url` change link to https:// to access IS 6.1 deployment on kubernetes

#### view all services

`kubectl get services`

#### delete cluster

`minikube delete --all`
