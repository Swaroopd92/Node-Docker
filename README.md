# Node-Docker
A dev/prod workflow using docker and Node.js

## Docker commands

### to see all the running containers
docker ps
### to see all the containers
docker ps -a 
### Builds an image named node-app-image with the Dockerfile in the current directry.
docker build -t node-app-image . 
### Creates a docker container where the volume /app/node_modules is not modified, but everything else in the current directory (%cd%) will be in sync with the /app directory. Specifying the /app volume to be read only to prevent the container from modifying the files. Asking docker to take the environment variables from the .env file. -p 5000:4000 is asking the docker to listen at 4000 and that the data comes form port 5000 from the local machine. --name is used to give docker container a name, and -d is to run in detach mode so that you are not attched to the docker CLI.
docker run -v %cd%:/app:ro -v /app/node_modules --env-file ./.env -p 5000:4000 -d --name node-app node-app-image
### this is to execute commands inside the docker container node-app
docker exec -it node-app bash
### Forces the deletion of the running container node-app -v is to delete the associated volume
docker rm node-app -fv
### Delete unused volume
docker volume prune
## Using docker-compose to run the container. Use --build to force a build
docker-compose up -d --build
