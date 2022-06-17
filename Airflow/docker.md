commands :

docker ps -l --format=$FORMAT

-l : last one

-a: all

$FORMAT is a costomized format for output



docker run -ti ubuntu:ubuntu_name

-ti: terminal interaction



error:

```java
Docker - Bind for 0.0.0.0:4000 failed: port is already allocated
```



Fix: 

```jva
docker container ls
docker stop <containerId>
```





