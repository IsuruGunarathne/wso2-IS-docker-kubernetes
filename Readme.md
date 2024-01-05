# Deploying and IS 6.1 docker image

## Deploying on docker

Copy the IS 6.1 folder (named wso2is-6.1.0) to the docker folder and run the following commands

#### Build image

`docker build -t is6.1 .` # image will be named IS6.1

#### Delete docker image

`docker rmi is6.1` # delete image named IS6.1
`docker rmi -f is6.1` # force delete image named IS6.1`

#### Run container

`docker run -d -p 127.0.0.1:9443:9443 is6.1` # run container in background and map port 8080 to 8080

#### logs for the container

`docker logs -f <container id>`
