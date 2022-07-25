https://sqbu-github.cisco.com/stap/airflow-platform-base/blob/develop/deploy/Dockerfile

```java
FROM registry-qa.webex.com/ubuntu/python38:v1.0.202110

COPY app/requirements.txt /app/requirements.txt
COPY app/constraints.txt /app/constraints.txt

RUN cd /app \
    && mkdir -p /usr/share/man/man1 \
    && apt update \
    && apt install --no-install-recommends -y python3-dev python3-pip unzip libaio1 gcc default-libmysqlclient-dev \
    && pip3 install wheel \
    && pip3 install --no-cache-dir -r requirements.txt --constraint constraints.txt \
    && apt remove -y gcc && apt autoremove -y && apt clean \
	&& mkdir -p /opt/oracle \
	&& wget -nv -P /opt/oracle https://download.oracle.com/otn_software/linux/instantclient/195000/instantclient-basiclite-linux.x64-19.5.0.0.0dbru.zip \
	&& unzip "/opt/oracle/instantclient*.zip" -d /opt/oracle \
	&& rm -f /opt/oracle/instantclient*.zip

COPY config/webserver_config.py /app/webserver_config.py
COPY config/matplotlibrc /app/.config/matplotlib/matplotlibrc

COPY --chown=ubuntu app/. /app

RUN chown ubuntu /app

ENV HOME=/app \
    AIRFLOW_HOME=/app \
    AIRFLOW__CORE__LOAD_EXAMPLES=False \
    AIRFLOW__CORE__LOAD_DEFAULT_CONNECTIONS=False \
    AIRFLOW__CORE__EXECUTOR=SequentialExecutor \
    AIRFLOW__CORE__SQL_ALCHEMY_CONN=sqlite:////app/airflow.db \
    AIRFLOW__SMTP__SMTP_HOST=mda.webex.com \
    AIRFLOW__SMTP__SMTP_MAIL_FROM=msq.airflow@cisco.com \
    AIRFLOW__CELERY__BROKER_URL='' \
    AIRFLOW__CELERY__RESULT_BACKEND=''

RUN airflow db init

ENV ORACLE_HOME=/opt/oracle/instantclient_19_5
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ORACLE_HOME \
    PATH=$ORACLE_HOME:$PATH

RUN usermod -u 10001 ubuntu
RUN airflow info
ENTRYPOINT ["/usr/local/bin/dumb-init","/main.sh"]
CMD ["airflow", "webserver"]
```



[airflow-platform-base](https://sqbu-github.cisco.com/stap/airflow-platform-base) (main): FROM registry-qa.webex.com/ubuntu/python38:v1.0.202110

Airflow-deploy-tasks (feature/new_build_deploy)(build):

(Jenkinsfile.main)  FROM registry-qa.webex.com/msq/airflow-platform-base:$AIRFLOW_PLATFORM_BASE_TAG



```java
ARG AIRFLOW_PLATFORM_BASE_TAG=latest
FROM registry-qa.webex.com/msq/airflow-platform-base:$AIRFLOW_PLATFORM_BASE_TAG

COPY tasks_requirements /app/tasks_requirements/

RUN set -o errexit; \
    apt update; apt install -y gcc; \
    for reqdir in /app/tasks_requirements /app/tasks_requirements/*; do \
        if [ -d $reqdir ];then \
            echo "Installing for $reqdir (apt)"; \
            export DEBIAN_FRONTEND=noninteractive; \
            test -f $reqdir/requirements.apt.txt \
                && apt update && apt install -y $(cat $reqdir/requirements.apt.txt) && apt clean; \
            echo "Installing for $reqdir (pip)"; \
            test -f $reqdir/requirements.pip.txt \
                && pip install --no-cache-dir -U -r $reqdir/requirements.pip.txt; \
            test -f $reqdir/requirements.txt \
                && pip install --no-cache-dir -U -r $reqdir/requirements.txt; \
        fi; \
    done; \
    echo "Cleaning up cache"; \
    apt remove -y gcc && apt autoremove -y && apt clean;

COPY dags /app/dags/
COPY plugins /app/plugins/
COPY tests /app/tests/
COPY utils /app/utils/
```

drwxrwxrwx.