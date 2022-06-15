error:

```java
Docker - Bind for 0.0.0.0:4000 failed: port is already allocated
```



Fix: 

```jva
docker container ls
docker stop <containerId>
```

