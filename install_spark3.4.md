Para instalar y configurar Apache Spark 3.4 en RHEL 8 y conectarlo a Hadoop 3.4, sigue estos pasos detallados:

### Prerrequisitos

1. **Java:** Asegúrate de tener Java instalado y configurado en todos los nodos.
2. **Hadoop:** Asegúrate de que Hadoop esté instalado y configurado correctamente en tu clúster.

### Descarga y Configuración de Apache Spark

1. **Descargar Apache Spark:**

   Descarga Apache Spark desde el sitio oficial. Puedes usar `wget` o `curl` para descargar el archivo tarball.

   ```bash
   wget https://downloads.apache.org/spark/spark-3.4.0/spark-3.4.0-bin-hadoop3.tgz
   ```

2. **Extraer el archivo tarball:**

   ```bash
   tar -xvzf spark-3.4.3-bin-hadoop3-scala2.13.tgz
   ```

3. **Mover el directorio de Spark a la ubicación deseada:**

   ```bash
   sudo mv spark-3.4.3-bin-hadoop3-scala2.13 /usr/local/spark
   ```

### Configuración de Variables de Entorno

Agrega las variables de entorno para Spark y Hadoop en tu archivo de configuración de shell, por ejemplo, `.bashrc` o `.bash_profile`.

1. **Editar el archivo `.bashrc`:**

   ```bash
   nano ~/.bashrc
   ```

2. **Agregar las siguientes líneas al final del archivo:**

   ```bash
   export HADOOP_HOME=/usr/local/hadoop
   export SPARK_HOME=/usr/local/spark
   export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$SPARK_HOME/bin:$SPARK_HOME/sbin
   ```

3. **Aplicar los cambios:**

   ```bash
   source ~/.bashrc
   ```

### Configuración de Spark

1. **Configurar `spark-env.sh`:**

   Copia el archivo de ejemplo y edítalo.

   ```bash
   cp $SPARK_HOME/conf/spark-env.sh.template $SPARK_HOME/conf/spark-env.sh
   nano $SPARK_HOME/conf/spark-env.sh
   ```

   Agrega las siguientes líneas para configurar Spark:

export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.412.b08-2.el8.x86_64/jre

   ```bash
export JAVA_HOME='/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.412.b08-2.el8.x86_64/jre'
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop

export SPARK_MASTER_HOST=172.27.251.21  # Cambia esta IP por la del servidor donde está el Spark Master
export SPARK_MASTER_PORT=7077           # Puerto donde escuchará el Spark Master
export SPARK_MASTER_WEBUI_PORT=8080     # Puerto para la interfaz web del Spark Master

# Establecer variables de entorno para Java (puedes ajustar según tu configuración de Java)
export SPARK_DIST_CLASSPATH=$(hadoop classpath)

# Configuración de la memoria para el driver y los ejecutores
export SPARK_DRIVER_MEMORY=2g
export SPARK_EXECUTOR_MEMORY=4g

# Configuración del directorio de trabajo de Spark (asegúrate de tener permisos)
export SPARK_WORKER_DIR=/var/lib/spark/work

# Configuración de Spark event log (opcional)
export SPARK_EVENT_LOG_ENABLED=true
export SPARK_EVENT_LOG_DIR=/var/log/spark/events
   ```

   Reemplaza `'your-master-node-hostname'` con el nombre del host de tu nodo maestro y `'/path/to/your/java'` con la ruta de tu instalación de Java.

2. **Configurar `slaves`:**

   Edita el archivo `slaves` para incluir los nombres de host o direcciones IP de tus nodos esclavos.

   ```bash
   nano $SPARK_HOME/conf/slaves
   ```

   Añade los nombres de host o direcciones IP, uno por línea:

   ```
   SRVMIGNODOWORKER1
   SRVMIGNODOWORKER2
   SRVMIGNODOWORKER3
   SRVMIGNODOWORKER4
   SRVMIGNODOWORKER5
   ```


# Habilitar permisos para carpeta work
ls -ld /usr/local/spark/work
sudo chown -R hadoopuser:hadoopuser /usr/local/spark/work
sudo chown -R hadoopuser:hadoopuser /usr/local/spark/logs

### Iniciar el clúster de Spark

1. **Iniciar el nodo maestro:**

   ```bash
   "$SPARK_HOME/sbin/start-master.sh"
   ```

2. **Iniciar los nodos esclavos:**

   ```bash
   $SPARK_HOME/sbin/start-workers.sh
   $SPARK_HOME/sbin/start-slaves.sh
   ```

### Verificación

1. **Verificar el estado del clúster:**

   Puedes acceder a la interfaz web de Spark para verificar el estado del clúster. Por defecto, está disponible en:

   ```
   http://your-master-node-hostname:8080
   ```

2. **Ejecutar una aplicación de prueba:**

   Para asegurarte de que todo esté configurado correctamente, puedes ejecutar una aplicación de prueba en Spark. Por ejemplo:

   ```bash
   $SPARK_HOME/bin/spark-submit --class org.apache.spark.examples.SparkPi --master spark://SRVMIGNODOWORKER1:7077 $SPARK_HOME/examples/jars/spark-examples_2.13-3.4.3.jar 100

   $SPARK_HOME/bin/spark-submit --class org.apache.spark.examples.SparkPi --master spark://SRVMIGNODOWORKER1:7077 $SPARK_HOME/examples/jars/spark-examples_2.12-3.4.0.jar 100

   $SPARK_HOME/bin/spark-submit --class org.apache.spark.examples.SparkPi --master spark://SRVMIGNODOWORKER1:7077 --executor-cores 4 $SPARK_HOME/examples/jars/spark-examples_2.13-3.4.3.jar 100

   ```

### Instalación de Herramientas Adicionales (Opcional)

Si necesitas instalar herramientas adicionales como ZooKeeper, Sqoop, Ranger, etc., asegúrate de seguir las guías específicas de instalación y configuración para cada una de estas herramientas, asegurándote de integrarlas correctamente con Hadoop y Spark.

Siguiendo estos pasos, deberías tener un clúster de Spark 3.4 funcionando correctamente en tu entorno RHEL 8, conectado a tu clúster Hadoop 3.4.



spark.jars.packages org.scala-lang:scala-library:2.12.15


HDFS: http://SRVMIGNODOWORKER1:9870
YARN ResourceManager: http://SRVMIGNODOWORKER1:8088
Spark Master UI: http://SRVMIGNODOWORKER1:8080




jdk.certpath.disabledAlgorithms=...
jdk.tls.disabledAlgorithms=...



YARN: http://172.27.251.21:8088/cluster/nodes
SPARK: http://172.27.251.21:8080/
HADOOP: http://172.27.251.21:9000/
ZEPPELIN: http://172.27.251.21:9997/
