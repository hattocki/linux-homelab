# Commands

## Install Docker
sudo apt update
sudo apt install docker.io -y

## Start Docker service
sudo systemctl start docker
sudo systemctl enable docker

## Verify Docker
docker --version
sudo systemctl status docker

## Run test container
sudo docker run hello-world

## Run Nginx container
sudo docker run -d -p 8080:80 nginx