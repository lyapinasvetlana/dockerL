# dockerL
//check 
docker ps -a
docker build -t lypinasveta/hamster .

data center - virtual machines - micro services 
не разносим на разные мащины, а на сервисы , потому что машины сложно поддерживать (разрешения, мониторинг), вертуализация сжирает много ресурсов.
приложение =кусок кода с приложениями - можно застваить его выполнять изолировано 
не запускает приложение на системе, а запускает процесс докера - внутри которого выполняется приложение.
каждое приложение закрыто, общаться можно только по сети (сетевой адрес) - как к другим машинам. 
Докер не эмулирует железо, он обеспечивает SECURITY и сеть.

Каждый контейнер содержит DockerFile 

--Оркестраутору - передаёте параметры элементы окружения - обеспечивает развернутый кластер. 

Docker Engine (программа на винде) - docker container (бегущий сервер) - использует docker image (небегущий сервер) - из чего состоит image = Dockerfile

https://user-images.githubusercontent.com/70142767/123624926-dd163680-d817-11eb-98e0-cf59df3db98a.png


#-------------------------------------------------
# Introduction to Docker by Denis Astahov


Install Docker on Ubuntu 18.04
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```
sudo apt update
sudo apt install apt-transport-https
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install docker-ce
sudo systemctl status docker
sudo usermod -aG docker $USER
>>>logout/login<<<
```

docker run hello-world
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

docker ps
docker ps -a
docker images


docker search tomcat
docker pull tomcat
docker run -it -p 1234:8080 tomcat
docker run -it -p 8888:80 nginx
docker run -d -p 8888:80 nginx



docker build -t denis .
docker images

docker run -it  -p 1234:80  denis:latest
docker run -d -p  1234:80  denis:latest

docker  ps     # list containers
docker  ps -a  # list all containers

docker tag denis_ubuntu denis_ubuntu-PROD
docker tag denis_ubuntu denis_ubuntu-PROD:v2

docker rm   # delete container
docker rmi  # delete image

UPDATE IMAGE
~~~~~~~~~~~~~
docker run -d -p 7777:80 denis_ubuntu4
docker exec -it 5267e21d140 /bin/bash
echo "V2" >> /var/www/html/index.html
exit
docker commit 5267e21d140 denis_v2:latest

Export/Import Docker Image to file
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
docker save image:tag > arch_name.tar
docker load -i arch_name.tar


Import/Export Docker Image to AWS ECR
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
docker build -t denis:v1 .
aws ecr get-login --no-include-email --region=ca-central-1 
docker tag  denis:v1  12345678.dkr.ecr.ca-central-1.amazonaws.com/myrepo:latest
docker push 12345678.dkr.ecr.ca-central-1.amazonaws.com/myrepo:lastest

docker pull 12345678.dkr.ecr.ca-central-1.amazonaws.com/myrepo:latest



Kill and Delete Containers and Images
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
docker rm -f $(docker ps -aq)        # Delete all Containers
docker rmi -f $(docker images -q)    # Delete all Images
