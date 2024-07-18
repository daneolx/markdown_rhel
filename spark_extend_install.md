Para configurar Spark 3.4.3 y Zeppelin 0.9 en un clúster con 5 nodos utilizando Hadoop 3.4 en RHEL 8, aquí tienes los pasos paso a paso:

### Configuración de Spark 3.4.3

#### 1. Descarga e Instalación de Spark

1. **Descarga Spark**: 
   - Ve al sitio de descargas de Apache Spark (https://spark.apache.org/downloads.html) y descarga la versión 3.4.3 precompilada para Hadoop 3.2 y superior.

2. **Extracción de Archivos**:
   - Copia el archivo descargado a cada nodo del clúster y extrae el contenido en un directorio deseado, por ejemplo, `/opt/spark-3.4.3`.

3. **Configuración de Variables de Entorno**:
   - Asegúrate de tener configuradas las variables de entorno relevantes (`SPARK_HOME`, `PATH`).

   ```bash
   export SPARK_HOME=/opt/spark-3.4.3
   export PATH=$PATH:$SPARK_HOME/bin
   ```

4. **Configuración de spark-env.sh**:
   - Copia el archivo `spark-env.sh.template` a `spark-env.sh` en la carpeta de configuración de Spark (`$SPARK_HOME/conf`) y configura las variables específicas de tu entorno (por ejemplo, configuraciones de memoria y Java).

   ```bash
   cp $SPARK_HOME/conf/spark-env.sh.template $SPARK_HOME/conf/spark-env.sh
   nano $SPARK_HOME/conf/spark-env.sh
   ```

   Ejemplo de configuración (`spark-env.sh`):

   ```bash
   export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-11.0.13.0.8-0.el8_5.x86_64
   export SPARK_MASTER_HOST=172.27.251.21
   export SPARK_MASTER_PORT=7077
   export SPARK_WORKER_INSTANCES=1
   export SPARK_WORKER_CORES=4
   export SPARK_WORKER_MEMORY=8g
   export SPARK_WORKER_DIR=/var/lib/spark/work
   ```

5. **Configuración spark-defaults.conf**:
   - Puedes ajustar configuraciones específicas de Spark en el archivo `spark-defaults.conf` en la carpeta de configuración (`$SPARK_HOME/conf`), como ajustes de memoria y configuraciones de ejecución.

   ```bash
   cp $SPARK_HOME/conf/spark-defaults.conf.template $SPARK_HOME/conf/spark-defaults.conf
   nano $SPARK_HOME/conf/spark-defaults.conf
   ```

   Ejemplo de configuración (`spark-defaults.conf`):

   ```properties
   spark.master            spark://172.27.251.21:7077
   spark.executor.memory   4g
   spark.driver.memory     2g
   ```

6. **Configuración de Workers**:
   - Edita el archivo `workers` en la carpeta de configuración de Spark (`$SPARK_HOME/conf`) y añade las direcciones IP o nombres de host de los nodos workers.

   ```bash
   nano $SPARK_HOME/conf/workers
   ```

   Ejemplo (`workers`):

   ```text
   SRVMIGNODOWORKER2
   SRVMIGNODOWORKER3
   SRVMIGNODOWORKER4
   SRVMIGNODOWORKER5
   ```

#### 2. Configuración de Hadoop para Spark

No se requieren cambios significativos en Hadoop 3.4 específicamente para Spark 3.4.3, ya que las versiones compatibles deben funcionar adecuadamente juntas.

### Configuración de Zeppelin 0.9

#### 1. Descarga e Instalación de Zeppelin

1. **Descarga Zeppelin**:
   - Descarga Zeppelin 0.9 desde el sitio oficial de Zeppelin (https://zeppelin.apache.org/download.html).

2. **Extracción de Archivos**:
   - Copia el archivo descargado a cada nodo del clúster y extrae el contenido en un directorio deseado, por ejemplo, `/opt/zeppelin-0.9`.

3. **Configuración de Variables de Entorno**:
   - Configura las variables de entorno relevantes para Zeppelin (`ZEPPELIN_HOME`, `PATH`).

   ```bash
   export ZEPPELIN_HOME=/opt/zeppelin-0.9
   export PATH=$PATH:$ZEPPELIN_HOME/bin
   ```

4. **Configuración zeppelin-env.sh**:
   - Copia el archivo `zeppelin-env.sh.template` a `zeppelin-env.sh` en la carpeta de configuración de Zeppelin (`$ZEPPELIN_HOME/conf`) y configura las variables específicas de tu entorno.

   ```bash
   cp $ZEPPELIN_HOME/conf/zeppelin-env.sh.template $ZEPPELIN_HOME/conf/zeppelin-env.sh
   nano $ZEPPELIN_HOME/conf/zeppelin-env.sh
   ```

   Ejemplo de configuración (`zeppelin-env.sh`):

   ```bash
   export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-11.0.13.0.8-0.el8_5.x86_64
   export MASTER=spark://172.27.251.21:7077
   ```

5. **Configuración de Zeppelin Interpreter**:
   - Configura los intérpretes de Zeppelin según sea necesario en la interfaz web de Zeppelin (`http://<zeppelin-server>:8080` por defecto).

6. **Inicio de Zeppelin**:
   - Inicia Zeppelin ejecutando el script `zeppelin-daemon.sh`:

   ```bash
   $ZEPPELIN_HOME/bin/zeppelin-daemon.sh start
   ```

### Consideraciones Finales

- Asegúrate de que los puertos necesarios (como el puerto 7077 para Spark Master) estén abiertos en los firewalls de los nodos.
- Verifica los logs de Spark y Zeppelin en caso de problemas durante la configuración o ejecución para obtener detalles adicionales sobre cualquier error.

Con estos pasos, deberías tener configurado un entorno básico de Spark 3.4.3 con Hadoop 3.4 y Zeppelin 0.9 en tu clúster de 5 nodos con RHEL 8. Ajusta las configuraciones según las necesidades específicas de tu entorno y carga de trabajo.