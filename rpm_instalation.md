## Validar version de java
update-alternatives --config java

Eliminar conflictos:
sudo rpm -e vim-minimal

Volver a instalar:
sudo rpm -ivh vim-minimal-8.2.2637-20.el9_1.x86_64.rpm

Forzar la instalación:
sudo rpm -ivh --replacefiles vim-minimal-8.2.2637-20.el9_1.x86_64.rpm


Actualizar el paquete:
sudo rpm -Uvh vim-minimal-8.2.2637-20.el9_1.x86_64.rpm


[MySQLServerConnection]
Driver=/opt/microsoft/msodbcsql18/lib64/libmsodbcsql-18.3.so.3.1
Server=172.27.0.124


###### docker shiro.ini

docker cp af8be48b1af5:/opt/zeppelin/conf/shiro.ini /opt/

docker cp /opt/shiro.ini af8be48b1af5:/opt/zeppelin/conf/


#####instalar Jars

driver sql -server

docker cp /opt/jars_install/mssql-jdbc-8.2.2.jre8.jar e8c590402b1c:/opt/zeppelin/lib/
docker cp /opt/jars_install/mssql-jdbc-8.2.2.jre8.jar e8c590402b1c:/opt/zeppelin/interpreter/spark

## Subir a Shiny

docker cp /opt/Shiny_deploy/DashMeses a97ffc6d4189:/opt/shiny-server/

docker cp /opt/jars_install/vegas_2.11-0.3.11.jar e8c590402b1c:/opt/zeppelin/lib/
docker cp /opt/jars_install/spark-sql_2.13-3.4.0.jar e8c590402b1c:/opt/zeppelin/lib/
docker cp /opt/jars_install/breeze-viz_2.12-1.1.jar e8c590402b1c:/opt/zeppelin/lib/
docker cp /opt/jars_install/breeze_2.12-1.1.jar e8c590402b1c:/opt/zeppelin/lib/
docker cp /opt/jars_install/breeze-natives_2.11-0.11.2.jar e8c590402b1c:/opt/zeppelin/lib/
docker cp /opt/jars_install/vegas_2.11-0.3.11-sources.jar e8c590402b1c:/opt/zeppelin/lib/
docker cp /opt/jars_install/vegas_2.11-0.3.11-javadoc.jar e8c590402b1c:/opt/zeppelin/lib/
docker cp /opt/jars_install/vegas-macros_2.11-0.3.7.jar e8c590402b1c:/opt/zeppelin/lib/

docker cp /opt/jars_install/vegas_2.11-0.3.11.jar e8c590402b1c:/opt/zeppelin/interpreter/spark
docker cp /opt/jars_install/breeze-viz_2.12-1.1.jar e8c590402b1c:/opt/zeppelin/interpreter/spark
docker cp /opt/jars_install/breeze_2.12-1.1.jar e8c590402b1c:/opt/zeppelin/interpreter/spark
docker cp /opt/jars_install/breeze-natives_2.11-0.11.2.jar e8c590402b1c:/opt/zeppelin/interpreter/spark
docker cp /opt/jars_install/vegas_2.11-0.3.11-sources.jar e8c590402b1c:/opt/zeppelin/interpreter/spark
docker cp /opt/jars_install/vegas_2.11-0.3.11-javadoc.jar e8c590402b1c:/opt/zeppelin/interpreter/spark
docker cp /opt/jars_install/vegas-macros_2.11-0.3.7.jar e8c590402b1c:/opt/zeppelin/interpreter/spark


vim /etc/odbc.ini


[MySqlServerDSN]
Driver=ODBC Driver 18 for SQL Server
Server=172.27.0.124
Port=1433
Database=SIM
UID=userestadistica
PWD=$Us3R_3sT4d1sTic4$


#### validar volumenes creados
docker volume list

docker volume rm jupyterhub_notebooks

docker volume create zeppelin_data ## creas un volumen de docker que actua como directorio que guarda todo sin eliminar al reiniciar docker

### comandos para levantar zeppelin añadiendo el volumen anteriormente creado 

docker run -d -v zeppelin_data:/opt/zeppelin/data -v zeppelin_notebook:/opt/zeppelin/notebook -p 9997:8080 apache_zeppelin_usr1:latest

docker volume inspect


### comandos para levantar zeppelin, jupyterhub 

docker run -d -v zeppelin_data:/opt/zeppelin/data -v zeppelin_notebook:/opt/zeppelin/notebook -p 9997:8080 apache_zeppelin_usr1:latest

docker exec -ti -u root e8c590402b1c /bin/bash

docker exec -ti -u root da01dc24726b /bin/bash

docker cp /opt/jars_install/mssql-jdbc-8.4.1.jre8.jar da01dc24726b:/opt/zeppelin/interpreter/spark/

## con jupyterhub iniciado - volumen: jupyterhub_notebooks

docker run -d -p 8000:8000 -v jupyterhub_notebooks:/srv/jupyterhub jupyterhub:lastest jupyterhub

## shiny -volumen: shiny_projects
docker run -d -p 3838:3838 \
    -v shiny_projects:/srv/shiny-server \
    rocker/shiny:latest


docker exec -ti -u root 0ad8f32a7027 /bin/bash
0ad8f32a7027

## R-Server - volumen: datos_rserver
docker run -d -p 8888:8787 \
    -v datos_rserver:/home/rstudio \
    rocker/rstudio:4.2.2

docker exec -ti -u root 09d268d34b75 /bin/bash



Red Hat Enterprise Linux release 9.3 (Plow)

dias_hora_2015   dias_hora_2016s  dias_hora_2018   dias_hora_2019s  dias_hora_2021   dias_hora_2022s
dias_hora_2015s  dias_hora_2017   dias_hora_2018s  dias_hora_2020   dias_hora_2021s
dias_hora_2016   dias_hora_2017s  dias_hora_2019   dias_hora_2020s  dias_hora_2022 



mv /opt/zeppelin/opt/zeppelin/data/* /opt/zeppelin/data/




docker cp e8c590402b1c:/opt/zeppelin/data/prueba_AIJCHLL027 /opt/jars_install/

docker cp e8c590402b1c:/opt/zeppelin/dfModTiempoAtencionSalidas /opt/jars_install/
docker cp e8c590402b1c:/opt/zeppelin/dias_hora_2015s /opt/jars_install/
docker cp e8c590402b1c:/opt/zeppelin/dias_hora_2016 /opt/jars_install/
docker cp e8c590402b1c:/opt/zeppelin/dias_hora_2016s /opt/jars_install/
docker cp e8c590402b1c:/opt/zeppelin/dias_hora_2017 /opt/jars_install/
docker cp e8c590402b1c:/opt/zeppelin/dias_hora_2017s /opt/jars_install/
docker cp e8c590402b1c:/opt/zeppelin/dias_hora_2018 /opt/jars_install/
docker cp e8c590402b1c:/opt/zeppelin/dias_hora_2018s /opt/jars_install/
docker cp e8c590402b1c:/opt/zeppelin/dias_hora_2019 /opt/jars_install/
docker cp e8c590402b1c:/opt/zeppelin/dias_hora_2019s /opt/jars_install/
docker cp 64eb3bb91845:/opt/zeppelin/dias_hora_2020 /opt/jars_install/
docker cp 64eb3bb91845:/opt/zeppelin/dias_hora_2020s /opt/jars_install/
docker cp 64eb3bb91845:/opt/zeppelin/dias_hora_2021 /opt/jars_install/
docker cp 64eb3bb91845:/opt/zeppelin/dias_hora_2021s /opt/jars_install/
docker cp 64eb3bb91845:/opt/zeppelin/dias_hora_2022 /opt/jars_install/
docker cp 64eb3bb91845:/opt/zeppelin/dias_hora_2022s /opt/jars_install/


docker cp /opt/jars_install/finalResultsE2020csv_temp da01dc24726b:/opt/zeppelin/data



docker cp /opt/Shiny_deploy/DashMovMigra/ 0ad8f32a7027:/srv/shiny-server/prueba


docker cp e8c590402b1c:/opt/zeppelin/servidores_hora /opt/jars_install/



docker cp e8c590402b1c:/opt/zeppelin/df_vuelos /opt/jars_install/
docker cp e8c590402b1c:/opt/zeppelin/df_vuelos_entrada /opt/jars_install/
docker cp e8c590402b1c:/opt/zeppelin/df_vuelos_salida /opt/jars_install/



docker cp e8c590402b1c:/opt/zeppelin/data/vuelos.parquet /opt/jars_install/

docker /home/dcantorin/vuelos.parquet 09d268d34b75/home/ecaceres/


docker cp 64eb3bb91845:/opt/zeppelin/dias_hora_2022s /opt/jars_install/


docker cp da01dc24726b:/opt/zeppelin/data/dfFlight /opt/jars_install/


docker cp da01dc24726b:/opt/zeppelin/final_ate_atsg /opt/jars_install/
docker cp da01dc24726b:/opt/zeppelin/final_sa_atsg /opt/jars_install/



## instalar offline R

wget https://cran.r-project.org/src/contrib/Matrix_1.6-0.tar.gz 

install.packages("/opt/Matrix_1.6-0.tar.gz", repos = NULL, type = "source")


