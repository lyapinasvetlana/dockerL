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
