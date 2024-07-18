Sí, puedes instalar y configurar un entorno de big data con las tecnologías que mencionas (Hadoop, ZooKeeper, Zeppelin, Hue, Spark, Ranger) sin necesidad de utilizar una distribución específica como Hortonworks. A continuación, te proporcionaré una guía general sobre cómo hacerlo:

### Prerequisitos

1. **Sistema Operativo**: Se recomienda usar una distribución de Linux (como Ubuntu o CentOS).
2. **Java**: Instala Java 8 o superior, ya que Hadoop y Spark requieren Java.
3. **SSH**: Asegúrate de tener configurado SSH para permitir la comunicación entre los nodos si estás configurando un clúster.

### Paso 1: Instalar Hadoop

1. **Descarga**: Descarga Hadoop 3.4 desde el sitio oficial de Apache Hadoop.
   ```bash
   wget https://downloads.apache.org/hadoop/common/hadoop-3.4.0/hadoop-3.4.0.tar.gz
   ```

2. **Extracción**: Extrae el archivo descargado.
   ```bash
   tar -xzvf hadoop-3.4.0.tar.gz
   ```

3. **Configuración**: Configura los archivos `core-site.xml`, `hdfs-site.xml`, `mapred-site.xml`, y `yarn-site.xml` en el directorio `etc/hadoop` de la instalación de Hadoop.

### Paso 2: Instalar ZooKeeper

1. **Descarga**: Descarga ZooKeeper desde el sitio oficial de Apache ZooKeeper.
   ```bash
   wget https://downloads.apache.org/zookeeper/zookeeper-3.7.2/apache-zookeeper-3.7.2-bin.tar.gz
   ```

2. **Extracción**: Extrae el archivo descargado.
   ```bash
   tar -xzvf apache-zookeeper-3.7.2-bin.tar.gz
   ```

3. **Configuración**: Configura el archivo `zoo.cfg` en el directorio `conf` de la instalación de ZooKeeper.

### Paso 3: Instalar Spark

1. **Descarga**: Descarga Spark 3.x desde el sitio oficial de Apache Spark.
   ```bash
   wget https://downloads.apache.org/spark/spark-3.4.3/spark-3.4.3-bin-hadoop3-scala2.13.tgz
   ```

2. **Extracción**: Extrae el archivo descargado.
   ```bash
   tar -xzvf spark-3.4.3-bin-hadoop3-scala2.13.tgz
   ```

### Paso 4: Instalar Zeppelin

1. **Descarga**: Descarga Zeppelin 0.11 desde el sitio oficial de Apache Zeppelin.
   ```bash
   wget https://downloads.apache.org/zeppelin/zeppelin-0.11.0/zeppelin-0.11.0-bin-all.tgz
   ```

2. **Extracción**: Extrae el archivo descargado.
   ```bash
   tar -xzvf zeppelin-0.11.0-bin-all.tgz
   ```

3. **Configuración**: Configura el archivo `zeppelin-site.xml` en el directorio `conf` de la instalación de Zeppelin.

### Paso 5: Instalar Hue

1. **Descarga y Configuración**: Sigue la [documentación oficial de Hue](https://docs.gethue.com/installation/).

### Paso 6: Instalar Ranger

1. **Descarga y Configuración**: Sigue la [documentación oficial de Apache Ranger](https://ranger.apache.org/).

wget https://www.apache.org/dist/ranger/2.4.0/apache-ranger-2.4.0.tar.gz
### Configuración Adicional

1. **Integración de Servicios**: Configura cada componente para que se comuniquen entre sí. Por ejemplo:
   - Configura Zeppelin para que utilice Spark como backend.
   - Configura Hue para que acceda a HDFS y otros servicios de Hadoop.
   - Configura Ranger para que controle el acceso a los recursos de Hadoop.

2. **Servicios y Daemons**: Inicia los servicios de Hadoop (namenode, datanode, resource manager, nodemanager), ZooKeeper, Spark, Zeppelin, y Hue.

### Ejemplo de Inicio de Servicios

```bash
# Hadoop
$HADOOP_HOME/sbin/start-dfs.sh
$HADOOP_HOME/sbin/start-yarn.sh

# ZooKeeper
$ZK_HOME/bin/zkServer.sh start

# Spark (standalone mode)
$SPARK_HOME/sbin/start-all.sh

# Zeppelin
$ZEPPELIN_HOME/bin/zeppelin-daemon.sh start

# Hue
hue runserver
```

### Notas Finales

- Asegúrate de seguir las guías de configuración de seguridad y optimización de cada componente para un entorno de producción.
- Considera la creación de scripts de automatización para facilitar el despliegue y administración del clúster.

Con estos pasos, deberías poder configurar un entorno de big data con las tecnologías mencionadas sin necesidad de utilizar Hortonworks.

## cluster
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.412.b08-2.el8.x86_64/jre
## nodito
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.412.b08-2.el9.x86_64/jre


PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/local/hadoop/bin:/usr/local/hadoop/sbin"JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.412.b08-2.el8.x86_64/jre"

mv hadoop-3.4.0 hadoop

172.27.251.21   SRVMIGNODOWORKER1
172.27.251.22   SRVMIGNODOWORKER2
172.27.251.23   SRVMIGNODOWORKER3
172.27.251.24   SRVMIGNODOWORKER4
172.27.251.25   SRVMIGNODOWORKER5


sudo chown -R hadoopuser:hadoopuser /usr/local/hadoop/
sudo chmod -R g+rwx /usr/local/hadoop/

scp -r /usr/local/hadoop/ hadoopuser@SRVMIGNODOWORKER2:/usr/local/
scp -r /usr/local/hadoop/ hadoopuser@SRVMIGNODOWORKER3:/usr/local/
scp -r /usr/local/hadoop/ hadoopuser@SRVMIGNODOWORKER4:/usr/local/
scp -r /usr/local/hadoop/ hadoopuser@SRVMIGNODOWORKER5:/usr/local/


scp -r /usr/local/hadoop/etc/hadoop/* hadoopuser@SRVMIGNODOWORKER2:/usr/local/hadoop/etc/hadoop/
scp -r /usr/local/hadoop/etc/hadoop/* hadoopuser@SRVMIGNODOWORKER3:/usr/local/hadoop/etc/hadoop/
scp -r /usr/local/hadoop/etc/hadoop/* hadoopuser@SRVMIGNODOWORKER4:/usr/local/hadoop/etc/hadoop/
scp -r /usr/local/hadoop/etc/hadoop/* hadoopuser@SRVMIGNODOWORKER5:/usr/local/hadoop/etc/hadoop/


ssh-copy-id hadoopuser@SRVMIGNODOWORKER1
ssh-copy-id hadoopuser@SRVMIGNODOWORKER2
ssh-copy-id hadoopuser@SRVMIGNODOWORKER3
ssh-copy-id hadoopuser@SRVMIGNODOWORKER4
ssh-copy-id hadoopuser@SRVMIGNODOWORKER5


sudo chmod +x /usr/local/hadoop/bin/hdfs
sudo chmod +x /usr/local/hadoop/bin/yarn


vim /usr/local/hadoop/etc/hadoop/core-site.xml
vim /usr/local/hadoop/etc/hadoop/yarn-site.xml


<configuration>
<property>
<name>fs.defaultFS</name>
<value>hdfs://SRVMIGNODOWORKER1:9000</value>
</property>
</configuration>


<configuration>
<property>
<name>dfs.namenode.name.dir</name><value>/usr/local/hadoop/data/nameNode</value>
</property>
<property>
<name>dfs.datanode.data.dir</name><value>/usr/local/hadoop/data/dataNode</value>
</property>
<property>
<name>dfs.replication</name>
<value>2</value>
</property>
</configuration>



scp /usr/local/hadoop/etc/hadoop/* SRVMIGNODOWORKER2:/usr/local/hadoop/etc/hadoop/


HDFS: http://localhost:9870 (Nombre del nodo)
YARN: http://localhost:8088 (Administrador de recursos de YARN)

ssh -v hadoopuser@SRVMIGNODOWORKER2


cd /usr/local/hadoop/etc/hadoop/


export HADOOP_HOME=/opt/hadoop
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin



### configurando el yarn

<property>
<name>yarn.resourcemanager.hostname</name>
<value>SRVMIGNODOWORKER1</value>
</property>


export PATH=$PATH:/usr/local/hadoop/sbin/start-yarn.sh


stop-dfs.sh
start-dfs.sh

stop-yarn.sh
start-yarn.sh


stop-all.sh
start-all.sh

## iniciar cluster

$HADOOP_HOME/sbin/start-all.sh

$SPARK_HOME/sbin/start-all.sh

/usr/local/zeppelin/bin/zeppelin-daemon.sh start

/opt/nifi/bin/nifi.sh start
