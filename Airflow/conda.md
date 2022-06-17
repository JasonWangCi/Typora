问题：

```java

jason@SENWAN-M-D1TF ~ % source activate base
source: no such file or directory: activate
```

解决：

```java
jason@SENWAN-M-D1TF ~ % conda activate base
source: no such file or directory: activate
```

原因，版本问题



```java
jason@SENWAN-M-D1TF ~ % conda info --envs
base                  *  /usr/local/anaconda3
airflow                  /usr/local/anaconda3/envs/airflow
airflow-docker-git       /usr/local/anaconda3/envs/airflow-docker-git
docker-compose           /usr/local/anaconda3/envs/docker-compose
```



问题

```java
jason@SENWAN-M-D1TF airflow-docker % conda info --env
zsh: command not found: conda
```

解决：

```java
jason@SENWAN-M-D1TF ~ % where conda                              
/usr/local/anaconda3/bin/conda
  
export PATH=/usr/local/anaconda3/bin:PATH
```

