### 1. Descargar e instalar Apache Zeppelin

#### Paso 1: Descarga Apache Zeppelin
Ve al nodo maestro (SRVMIGNODOWORKER1) y descarga Apache Zeppelin:

```sh
wget https://downloads.apache.org/zeppelin/zeppelin-0.10.0/zeppelin-0.10.0-bin-all.tgz
```

#### Paso 2: Extrae el archivo descargado

```sh
tar -xvf zeppelin-0.9.0-bin-all.tgz
mv zeppelin-0.9.0-bin-all /usr/local/zeppelin
```

sudo chown -R hadoopuser:hadoopuser /usr/local/zeppelin
sudo chmod -R g+rwx /usr/local/zeppelin/

#### Paso 3: Configura Zeppelin

Crea un archivo de configuración `zeppelin-env.sh` en el directorio `conf` de Zeppelin:

sudo chown -R hadoopuser:hadoopuser /usr/local/

```sh
cd /usr/local/zeppelin/conf
cp zeppelin-env.sh.template zeppelin-env.sh
```

Edita `zeppelin-env.sh` para que contenga las siguientes líneas:

```sh

export JAVA_HOME='/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.412.b08-2.el8.x86_64/jre'
export HADOOP_CONF_DIR=/usr/local/hadoop/etc/hadoop
export ZEPPELIN_PORT=9997
export SPARK_HOME=/usr/local/spark
export USE_HADOOP=true
export SPARK_MASTER=spark://172.27.251.21:7077
export ZEPPELIN_ADDR=0.0.0.0
export ZEPPELIN_INTERPRETER_OUTPUT_LIMIT=1048576
export PYSPARK_PYTHON=python3
export PYSPARK_DRIVER_PYTHON=python3



```

### 2. Configurar Zeppelin para usar Spark en el clúster

#### Paso 1: Configura el intérprete de Spark

Edita el archivo de configuración del intérprete de Zeppelin `conf/interpreter.json` para asegurarte de que está configurado correctamente para Spark. 


sudo chown -R hadoopuser:hadoopuser /usr/local/zeppelin/

sudo chmod -R 755 /usr/local/zeppelin/

Ejemplo de configuración mínima para Spark:

```json
{
  "name": "spark",
  "properties": {
    "spark.master": {
      "name": "spark.master",
      "type": "string",
      "value": "spark://SRVMIGNODOWORKER1:7077"
    },
    "spark.submit.deployMode": {
      "name": "spark.submit.deployMode",
      "type": "string",
      "value": "client"
    },
    "spark.driver.memory": {
      "name": "spark.driver.memory",
      "type": "string",
      "value": "40g"
    },
    "spark.executor.memory": {
      "name": "spark.executor.memory",
      "type": "string",
      "value": "10g"
    }
  }
}
```

### 3. Iniciar Apache Zeppelin

Ve al directorio de instalación de Zeppelin y ejecuta el script de inicio:

```sh
cd /usr/local/zeppelin
bin/zeppelin-daemon.sh start
```

### 4. Verificar la instalación

Abre tu navegador web y dirígete a `http://SRVMIGNODOWORKER1:9997`. Deberías ver la interfaz de Apache Zeppelin.

### 5. Ejecutar un trabajo de prueba en Zeppelin

1. Crea un nuevo notebook en Zeppelin.
2. Selecciona el intérprete de Spark.
3. Escribe el siguiente código en una celda y ejecútalo para probar la integración con Spark:

```scala
%spark
val data = Seq((1, "Spark"), (2, "Zeppelin"), (3, "Hadoop"))
val df = spark.createDataFrame(data).toDF("id", "name")
df.show()
```

Esto debería mostrar un pequeño DataFrame con los datos especificados.

### 6. Configurar Zeppelin en modo distribuido (opcional)

Si deseas que Zeppelin también funcione en modo distribuido, asegurándote de que los nodos del clúster pueden ejecutar los intérpretes de Zeppelin, necesitarás configurar el `zeppelin-site.xml` en el directorio `conf` de Zeppelin:

```xml
<configuration>
    
    <property>
        <name>zeppelin.server.port</name>
        <value>8080</value>
    </property>
    <property>
        <name>zeppelin.server.rpc.portRange</name>
        <value>5000-5100</value>
    </property>
    <property>
        <name>zeppelin.interpreter.rpc.portRange</name>
        <value>6000-6100</value>
    </property>
    <property>
        <name>zeppelin.notebook.dir</name>
        <value>/usr/local/zeppelin/notebook</value>
    </property>
</configuration>

<configuration>
  <!-- Configuration for Zeppelin server -->
  <property>
    <name>zeppelin.server.port</name>
    <value>8080</value>
    <description>Zeppelin server port</description>
  </property>

  <!-- Configuration for Hadoop -->
  <property>
    <name>zeppelin.hadoop.home</name>
    <value>/usr/local/hadoop</value>
    <description>Hadoop home directory</description>
  </property>

<!-- Configuration for Spark -->
<property>
<name>zeppelin.spark.master</name>
<value>yarn</value>
<description>Master for Spark, use yarn for Hadoop integration</description>
</property>
<property>
<name>zeppelin.spark.submit.deployMode</name>
<value>cluster</value>
<description>Deployment mode for Spark interpreter</description>
</property>
<property>
<name>zeppelin.spark.yarn.queue</name>
<value>default</value>
<description>Yarn queue for Spark interpreter</description>
</property>
<property>
<name>zeppelin.spark.useHiveContext</name>
<value>true</value>
<description>Use HiveContext instead of SQLContext if hive dependencies are loaded</description>
</property>

  <!-- Configuración del clúster de Zeppelin -->
  <property>
    <name>zeppelin.cluster.enabled</name>
    <value>true</value>
    <description>Enable cluster mode</description>
  </property>
  <property>
    <name>zeppelin.cluster.address</name>
    <value>172.27.251.21</value>
    <description>Cluster master address</description>
  </property>
  <property>
  <name>zeppelin.cluster.addr</name>
  <value>172.27.251.21:6000,172.27.251.22:6000,172.27.251.23:6000,172.27.251.24:6000,172.27.251.25:6000</value>
  <description>Server cluster address, eg. 127.0.0.1:6000,127.0.0.2:6000,127.0.0.3:6000</description>
</property>
  <property>
    <name>zeppelin.cluster.port</name>
    <value>8080</value>
    <description>Cluster master port</description>
  </property>
  <property>
    <name>zeppelin.notebook.dir</name>
    <value>/usr/local/zeppelin/notebook</value>
    <description>Directory for storing notebooks</description>
  </property>

  <!-- Additional configurations -->
  <property>
    <name>zeppelin.notebook.storage</name>
    <value>org.apache.zeppelin.notebook.repo.GitNotebookRepo</value>
    <description>Notebook storage class</description>
  </property>
  <property>
    <name>zeppelin.notebook.git.remote.url</name>
    <value>https://github.com/user/repo.git</value>
    <description>Git remote URL for notebook storage</description>
  </property>
  <property>
    <name>zeppelin.notebook.dir</name>
    <value>/usr/local/zeppelin/notebook</value>
    <description>Directory for storing notebooks</description>
  </property>
</configuration>

```

Después de realizar estos pasos, Apache Zeppelin debería estar listo para usar con Spark en tu clúster. ¡Buena suerte!

vim zeppelin-env.sh

export JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.412.b08-2.el8.x86_64/jre/"
export USE_HADOOP=true
export SPARK_MASTER=spark://172.27.251.21:7077
export ZEPPELIN_ADDR=0.0.0.0
export ZEPPELIN_PORT=9997
export SPARK_HOME=/usr/local/spark
export HADOOP_CONF_DIR=/usr/local/hadoop/etc/hadoop
export ZEPPELIN_JAVA_OPTS="-Dspark.driver.memory=40g -Dspark.executor.memory=10g"


cp shiro.ini.template shiro.ini
vim shiro.ini


/usr/local/zeppelin/bin/zeppelin-daemon.sh stop
/usr/local/zeppelin/bin/zeppelin-daemon.sh start


ls -l /usr/local/zeppelin/interpreter/spark/

sudo chown -R hadoopuser:hadoopuser /usr/local/zeppelin/interpreter/spark/

### AÑADIR A BASH

vim ~/.bashrc

export ZEPPELIN_HOME=/usr/local/zeppelin

source ~/.bashrc

$ZEPPELIN_HOME/bin/zeppelin-daemon.sh restart
