# Docker – Birinci Bölüm

## Docker Nedir?
## Docker Nasıl Çalışır?
## Docker Nerede Kullanılır?

| 	 Komut       | Açıklama     |
| :------------- | :----------: |
|  docker images | Lokal registry’de mevcut bulunan Image’ları listeler  |
| docker ps	     | Halihazırda çalışmakta olan Container’ları listeler |
|docker ps -a||
|docker ps -aq||
|docker pull <repository_name>/<image_name>:<image_tag>||
|docker top <container_id>||
|docker run -it <image_id/image_name> CMD||
|docker pause <container_id>||
|docker unpause <container_id>||
|docker stop <container_id>||
|docker start <container_id>||
|docker rm <container_id>||
|docker rm -v <container_id>||
|docker rm -f <container_id>||
|docker rmi <image_id/image_name>||
|docker rmi -f <image_id/image_name>||
|docker info||
|docker inspect <container_id>||
|docker inspect <image_id/image_name>||
|docker rm $(docker ps -aq)||
|docker stop $(docker ps -aq)||
|docker rmi $(docker images -aq)||
|docker images -q -f dangling=true||
|docker rmi $(docker images -q -f dangling=true)||
|docker volume ls -f dangling=true||
|docker volume rm $(docker volume ls -f dangling=true -q)||
|docker logs <container_id>||
|docker logs -f <container_id>||
|docker exec <container_id> <command>||
|docker exec -it <container_id> /bin/bash||
|docker attach <container_id>||
