python3 -m venv airflow_venv
source airflow_venv/bin/activate


Instalar Apache Airflow:

export AIRFLOW_HOME=~/airflow
export AIRFLOW_VERSION=2.6.1
export PYTHON_VERSION="$(python --version | cut -d " " -f 2 | cut -d "." -f 1-2)"
export CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"

Instala Apache Airflow usando pip con las restricciones especificadas:

pip install "apache-airflow==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"


Inicializar la base de datos de Airflow:

airflow db init

Crear un usuario administrador:

airflow users create \
  --username admin \
  --firstname David \
  --lastname Cantorin \
  --role Admin \
  --email dcantorin@migraciones.gob.pe


Iniciar el servidor web de Airflow:

airflow webserver --port 8080


Iniciar el scheduler de Airflow:

airflow scheduler


### para detener proceso

pkill -f "airflow webserver"

pkill -f "airflow scheduler"



