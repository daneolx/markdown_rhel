El mensaje indica que Scala no está instalada o no está en el PATH de tu sistema. A continuación, te guiaré a través de los pasos necesarios para instalar Scala 2.12 en RHEL 8 y configurarlo adecuadamente.

### Paso 1: Descargar e Instalar Scala 2.12

1. Descarga Scala 2.12 desde el sitio oficial de Scala:

```sh
wget https://downloads.lightbend.com/scala/2.12.15/scala-2.12.15.tgz
```

2. Extrae el archivo descargado:

```sh
tar xvf scala-2.12.15.tgz
```

3. Mueve Scala a un directorio adecuado, por ejemplo, `/usr/local/scala`:

```sh
sudo mv scala-2.12.15 /usr/local/scala-2.12.15
```

### Paso 2: Configurar las Variables de Entorno

1. Abre tu archivo de perfil (`~/.bashrc`, `~/.bash_profile`, o `~/.profile` dependiendo de tu shell).

2. Añade las siguientes líneas para configurar `SCALA_HOME` y actualizar `PATH`:

```sh
export SCALA_HOME=/usr/local/scala-2.12.15
export PATH=$SCALA_HOME/bin:$PATH
```

3. Recarga tu archivo de perfil para aplicar los cambios:

```sh
source ~/.bashrc  # o el archivo que hayas modificado
```

### Paso 3: Verificar la Instalación

Verifica que Scala se haya instalado correctamente:

```sh
scala -version
```

Deberías ver una salida similar a:

```sh
Scala code runner version 2.12.15 -- Copyright 2002-2021, LAMP/EPFL
```

### Paso 4: Configurar Zeppelin para Usar Scala 2.12

1. Abre el archivo de configuración de Zeppelin `zeppelin-env.sh`, que suele estar en el directorio de configuración de Zeppelin, por ejemplo, `/usr/local/zeppelin/conf/zeppelin-env.sh`.

2. Añade o modifica las siguientes líneas para asegurarte de que las rutas y versiones sean correctas:

```sh
export SCALA_HOME=/usr/local/scala-2.12.15
export SCALA_VERSION=2.12.15
export SPARK_HOME=/usr/local/spark
```

Asegúrate de reemplazar `/path/to/your/spark-3.4.3` con la ruta correcta a tu instalación de Spark.

### Paso 5: Configurar el Intérprete de Spark en Zeppelin

1. Abre la interfaz de Zeppelin en tu navegador (`http://<master-node-ip>:8080`).
2. Ve a la sección **Interpreter** (`http://<master-node-ip>:8080/#/interpreter`).
3. Selecciona el intérprete `spark` y verifica o añade las siguientes propiedades:

```plaintext
spark.jars.packages org.scala-lang:scala-library:2.12.15
```

### Paso 6: Reiniciar Zeppelin

Reinicia Zeppelin para aplicar los cambios de configuración:

```sh
/usr/local/zeppelin/bin/zeppelin-daemon.sh restart
```

### Paso 7: Verificar la Configuración

Abre un nuevo notebook en Zeppelin y ejecuta los siguientes comandos para verificar que estás usando las versiones correctas de Scala y Spark:

```scala
// Verificar la versión de Scala
println(scala.util.Properties.versionString)

// Verificar la versión de Spark
println(spark.version)
```

### Resumen

Siguiendo estos pasos, deberías poder instalar y configurar Scala 2.12 en tu sistema, ajustar Zeppelin para usar la versión correcta de Scala y resolver el problema de incompatibilidad de la versión de Scala con Spark 3.4.3.