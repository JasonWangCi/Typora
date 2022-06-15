![image-20220615094331817](/Users/jason/Library/Application Support/typora-user-images/image-20220615094331817.png)

![image-20220615094504440](/Users/jason/Library/Application Support/typora-user-images/image-20220615094504440.png)



Step 1:

启动docker容器

Step 2:

新建/启动 airflow环境

Step 3：

在docker-compose.yml文件目录下，新建 dags, logs, plugins文件夹

Step 4:

echo -e "AIRFLOW_UID=$(id -u) \nAIRFLOW GID=0" -env

Step 5:

初始化airflow ： docker-compose up airflow-init

Step 6:

启动服务（localhost:8080） docker-compose up





