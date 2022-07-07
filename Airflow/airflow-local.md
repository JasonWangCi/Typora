conda env create -n airflow2 python=3.6





source activate airflow2
export AIRFLOW_HOME=~/airflow
AIRFLOW_VERSION=2.1.3
PYTHON_VERSION="$(python --version | cut -d " " -f 2 | cut -d "." -f 1-2)"
CONSTRAINT_URL="constraints.txt"
pip install "apache-airflow==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"
pip install -r requirements.txt





airflow db init



airflow users create --username admin --firstname Jason --lastname Wang --role Admin --email senwan@cisco.com



airflow webserver --port 8080

airflow scheduler