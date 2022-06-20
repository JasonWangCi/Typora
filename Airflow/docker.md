commands :

```java
docker ps -l --format=$FORMAT

-l : last one

-a: all

$FORMAT is a costomized format for output



docker run -ti ubuntu:ubuntu_name bash

-ti: terminal interaction



Docker commit docker_id

docker tag xxxxx  costomized_name
```





![image-20220617085446301](/Users/jason/Library/Application Support/typora-user-images/image-20220617085446301.png)

repository : where the image come from  , eg: mysql, redis, airflow, etc

tag: version of the image



查询containers

docker container ls

停止： docker stop container_id 

删除container：

docker rm container_id

强制删除： docker rm -f container_id

删除所有contaniner： docker rm -f $(docker ps -a -q)



docker build -t hello .

docker images 

docker container ls

docker run --rm -ti ubuntu 



`[host port]:[container port]`.







error:

```java
Docker - Bind for 0.0.0.0:4000 failed: port is already allocated
```



Fix: 

```jva
docker container ls
docker stop <containerId>
```





