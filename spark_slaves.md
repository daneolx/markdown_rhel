### Instalación de Spark en los Nodos Esclavos

1. **Copia el archivo tarball de Spark a cada nodo esclavo:**

   Usa `scp` para copiar el archivo tarball de Spark a los nodos esclavos.

   ```bash
   scp spark-3.4.0-bin-hadoop3.tgz hadoopuser@SRVMIGNODOWORKER2:/home/hadoopuser/
   scp spark-3.4.0-bin-hadoop3.tgz hadoopuser@SRVMIGNODOWORKER3:/home/hadoopuser/
   scp spark-3.4.0-bin-hadoop3.tgz hadoopuser@SRVMIGNODOWORKER4:/home/hadoopuser/
   scp spark-3.4.0-bin-hadoop3.tgz hadoopuser@SRVMIGNODOWORKER5:/home/hadoopuser/


   scp spark-3.4.3-bin-hadoop3-scala2.13.tgz hadoopuser@SRVMIGNODOWORKER2:/home/hadoopuser/
   ```

   scp /usr/local/spark/ hadoopuser@SRVMIGNODOWORKER2:/usr/local/

2. **Instala Spark en cada nodo esclavo:**

   Inicia sesión en cada nodo esclavo y descomprime el archivo tarball.

   ```bash
   ssh hadoopuser@SRVMIGNODOWORKER2
   tar -xvzf /home/hadoopuser/spark-3.4.3-bin-hadoop3-scala2.13.tgz
   sudo mv spark-3.4.3-bin-hadoop3-scala2.13 /usr/local/spark
   exit

   ssh hadoopuser@SRVMIGNODOWORKER3
   tar -xvzf /home/hadoopuser/spark-3.4.0-bin-hadoop3.tgz
   sudo mv spark-3.4.0-bin-hadoop3 /usr/local/spark
   exit

   ssh hadoopuser@SRVMIGNODOWORKER4
   tar -xvzf /home/hadoopuser/spark-3.4.0-bin-hadoop3.tgz
   sudo mv spark-3.4.0-bin-hadoop3 /usr/local/spark
   exit

   ssh hadoopuser@SRVMIGNODOWORKER5
   tar -xvzf /home/hadoopuser/spark-3.4.0-bin-hadoop3.tgz
   sudo mv spark-3.4.0-bin-hadoop3 /usr/local/spark
   exit
   ```

### Configuración de Variables de Entorno en los Nodos Esclavos

1. **Edita el archivo `.bashrc` para configurar las variables de entorno en cada nodo esclavo:**

   ```bash
   ssh hadoopuser@SRVMIGNODOWORKER2
   nano su - hadoo

   # Añadir las siguientes líneas
   export SPARK_HOME=/usr/local/spark
   export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin

   # Aplicar los cambios
   source ~/.bashrc
   exit

   ssh hadoopuser@SRVMIGNODOWORKER3
   nano ~/.bashrc

   # Añadir las siguientes líneas
   export SPARK_HOME=/usr/local/spark
   export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin

   # Aplicar los cambios
   source ~/.bashrc
   exit

   ssh hadoopuser@SRVMIGNODOWORKER4
   nano ~/.bashrc

   # Añadir las siguientes líneas
   export SPARK_HOME=/usr/local/spark
   export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin

   # Aplicar los cambios
   source ~/.bashrc
   exit

   ssh hadoopuser@SRVMIGNODOWORKER5
   nano ~/.bashrc

   # Añadir las siguientes líneas
   export SPARK_HOME=/usr/local/spark
   export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin

   # Aplicar los cambios
   source ~/.bashrc
   exit
   ```

### Iniciar los Trabajadores de Spark

Una vez que Spark esté instalado y configurado en todos los nodos esclavos, puedes iniciar los trabajadores de Spark.

1. **Usa el script `start-workers.sh` en el nodo maestro:**

   ```bash
   $SPARK_HOME/sbin/start-workers.sh
   ```

Este comando iniciará los trabajadores de Spark en todos los nodos esclavos especificados en el archivo `slaves` o `workers`.

### Verificación

Accede a la interfaz web de Spark para verificar que los trabajadores estén conectados y funcionando correctamente:

```
http://172.27.251.21:8080/
```

Con estos pasos, debes tener un clúster de Spark funcionando correctamente con todos los nodos esclavos conectados.