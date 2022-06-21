```jav
pip install celery
```

```java
https://helm.sh/docs/intro/quickstart/
```



新建环境

```sql
conda create -n env_name python=3.6 pandas=0.21
```

查看环境

```java
conda info --env
```

激活环境

```sql
conda activate <env_name>
```



导出conda 环境配置

```bash
conda env export > environment.yml
```



复制已存在的环境

```sql
conda create -n new_env_name --clone old_env_name
```



导入环境配置

```sql
conda env create -f environment.yml
```



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

强制删除所有images： docker rmi -f $(docker images -aq)



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



修改airflow默认的sqllite to mysql

```
mysql+mysqldb://<user>:<password>@<host>[:<port>]/<dbname>
```

```
修改：sql_alchemy_conn = mysql+mysqldb://root:password@mysqlip:3306/airflow
```
