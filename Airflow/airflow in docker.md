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



