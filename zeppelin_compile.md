Compilar Apache Zeppelin desde el código fuente es un proceso que implica varios pasos, incluyendo la preparación del entorno, la descarga del código fuente, y la compilación misma. Aquí tienes los pasos detallados para compilar Zeppelin desde el código fuente:

### Requisitos Previos

Antes de comenzar, asegúrate de tener instalado lo siguiente:

1. **Java Development Kit (JDK)**: Zeppelin requiere Java 8 o superior. Asegúrate de tener el JDK instalado y configurado correctamente en tu sistema.

   ```bash
   sudo yum install java-devel    # Instalar JDK en RHEL
   ```

2. **Apache Maven**: Maven se utiliza para compilar proyectos Java. Asegúrate de tener Maven instalado.

   ```bash
   sudo yum install maven         # Instalar Maven en RHEL
   ```

3. **Git**: Necesitarás Git para clonar el repositorio de Zeppelin.

   ```bash
   sudo yum install git           # Instalar Git en RHEL
   ```

### Pasos para Compilar Zeppelin

1. **Clonar el Repositorio de Zeppelin**:

   Clona el repositorio de Zeppelin desde GitHub:

   ```bash
   git clone https://github.com/apache/zeppelin.git
   ```

   Esto creará un directorio `zeppelin` en tu ubicación actual.

2. **Navegar al Directorio de Zeppelin**:

   Cambia al directorio `zeppelin` que acabas de clonar:

   ```bash
   cd zeppelin
   ```

3. **Compilar Zeppelin**:

   Utiliza Maven para compilar Zeppelin. Puedes compilarlo con soporte para diferentes intérpretes según sea necesario. Por ejemplo, para compilar con soporte para Spark y Hadoop:

   ```bash
   mvn clean package -Pspark-3.4 -Dspark.version=3.4.0 -Phadoop-3.4 -Dhadoop.version=3.4.0 -Pscala-2.12 -Dscala.version=2.12.17 -DskipTests

   mvn clean package -Pspark-3.4 -Dspark.version=3.4.0 -Phadoop-3.4 -Dhadoop.version=3.4.0 -Pscala-2.12 -Dscala.version=2.12.17 -Pr -Ppyspark -DskipTests

   mvn clean package -Pspark-3.4 -Dspark.version=3.4.0 -Phadoop-3.4 -Dhadoop.version=3.4.0 -Pscala-2.12 -Dscala.version=2.12.17 -Pr -Ppyspark -DskipTests


   ```

   - `-Pspark-3.4`: Habilita el perfil para Spark 3.4 (ajusta según tu versión de Spark).
   - `-Dspark.version=3.4.0`: Especifica la versión de Spark que estás utilizando.
   - `-Phadoop-3.4`: Habilita el perfil para Hadoop 3.2 (ajusta según tu versión de Hadoop).
   - `-Dhadoop.version=3.4.0`: Especifica la versión de Hadoop que estás utilizando.
   - `-Pscala-2.12`: Habilita el perfil para Scala 2.12 (ajusta según tu versión de Scala).
   - `-Dscala.version=2.12.17`: Especifica la versión de Scala que estás utilizando.
   - `-DskipTests`: Opcionalmente, puedes omitir la ejecución de pruebas unitarias para acelerar la compilación inicial.

   Este comando compilará Zeppelin con soporte para Spark, Hadoop y Scala según las versiones especificadas.

4. **Configurar Zeppelin (opcional)**:

   Después de la compilación, puedes configurar Zeppelin según tus necesidades en el archivo de configuración `conf/zeppelin-site.xml`.

5. **Iniciar Zeppelin**:

   Una vez compilado, puedes iniciar Zeppelin ejecutando el siguiente comando desde el directorio raíz de Zeppelin:

   ```bash
   ./bin/zeppelin-daemon.sh start
   ```

6. **Acceder a Zeppelin**:

   Abre un navegador web y accede a la interfaz web de Zeppelin utilizando la dirección `http://localhost:8080` (o la dirección y puerto configurados según tu entorno).

### Notas Adicionales

- **Compilación con otros intérpretes**: Si necesitas soporte para otros intérpretes (por ejemplo, Flink, JDBC, etc.), ajusta los perfiles y versiones según sea necesario en el comando de compilación Maven.

- **Dependencias**: Asegúrate de que todas las dependencias requeridas estén instaladas y configuradas correctamente antes de la compilación.

Siguiendo estos pasos, deberías poder compilar Apache Zeppelin desde el código fuente en tu entorno RHEL8 con Scala 2.12.17, Spark 3.4.0 y otras configuraciones necesarias.


## Iniciar GRAFANA

 cd /usr/local
  982  ls
  983  clear
  984  ls
  985  cd grafana
  986  ls
  987  ./bin/grafana-server web
