#DockerFile
FROM ubuntu:20.04 //навзвание images

RUN apt-get -y update
RUN apt-get -y install apache2

RUN echo 'Hello World from Docker!' > /var/www/html/index.html


CMD ["/usr/sbin/apache2ctl", "-D","FOREGROUND"] /-D = background
EXPOSE 80 //открываем 80 порт


//delete all
docker rm -vf $(docker ps -a -q)
docker rmi -f $(docker images -a -q)


///push
docker tag lol:version2 lyapinasveta/fordocker:latest
docker push lyapinasveta/fordocker

//pull
docker pull lyapinasveta/fordocker

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
sudo systemctl status docker //sudo service docker status
docker -v
**запуск докера
sudo usermod -aG docker $USER
sudo dockerd

>>>logout/login<<<
```
//ищет есть ли данный image (run) - если находит запускает
docker run hello-world
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

docker ps //бегущие контейнеры
docker ps -a
//смотреть какие есть images
docker images //внутри секьюрити и сервис упакован
 
//запустить веб-сервис готовый из DockerHub
docker search tomcat

//просто скачать image
docker pull tomcat

ifvonfig //проверяем ip  адрес
//запустить контейнер
///если вы однажды запустили docker run и остановили его, то в следующий раз его уже нужно запускать через docker start, иначе запуская docker run каждый раз, вы будете плодить одинаковые контейнеры

//-p перенаправление портов - перенаправили на 1234
docker run -it -p 1234:8080 tomcat //it - интерактивно

docker run -it -p 8888:80 nginx
docker run -d -p 8888:80 nginx // -d - бегут в бэкграунде
 ///localhost:порт

*********
создадим директорию
mkdir mydocker
cd mydocker
ll
//текстовый редактор
nano DockerFile
****************


docker build -t denis . //создать image / . =искать локально
docker images

docker run -it  -p 1234:80  denis:latest
docker run -d -p  1234:80  denis:latest

docker  ps     # list containers
docker  ps -a  # list all containers

//копирование с изменением Name
docker tag denis_ubuntu denis_ubuntu-PROD
docker tag denis_ubuntu denis_ubuntu-PROD:v2

//удалить 
docker rm   # delete container
docker rmi  # delete image

UPDATE IMAGE
~~~~~~~~~~~~~
docker run -d -p 7777:80 denis_ubuntu4
docker exec -it 5267e21d140 /bin/bash
//добавили сообщение в html
echo "V2" >> /var/www/html/index.html
exit
//из бегущего контейнера делаем images - conainer id - name of new image 
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

//login на контейнер
docker
