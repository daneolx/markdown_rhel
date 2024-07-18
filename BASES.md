sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="10.100.0.111" port port="8000" protocol="tcp" accept'

### HABILITAR TELNET
dism /online /Enable-Feature /FeatureName:TelnetClient

### AÑADIR PUERTOS DE CONFIANZA
sudo firewall-cmd --permanent --add-port=91/tcp
sudo firewall-cmd --reload


curl -sL https://deb.nodesource.com/setup_14.x | bash -apt-get install -y nodejs

systemctl firewalld restart

### VALIDAR MAQUINA VIRTUAL

sudo dmidecode -s system-manufacturer


### Validar kernel 

jupyter console --kernel=python3


#####
source /opt/jupyterhub-venv/bin/activate

useradd -m -s /bin/bash jupyterhub

jupyterhub --generate-config

####copy redhat to docker 

docker cp /opt/jars_install/sqljdbc42-6.0.8112.jar c8e18e162509:/opt/zeppelin/

sudo tee /etc/systemd/system/jupyterhub.service <<EOF
[Unit]
Description=JupyterHub
After=network.target

[Service]
User=jupyterhub
Environment="PATH=/opt/jupyterhub-venv/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
ExecStart=/opt/jupyterhub-venv/bin/jupyterhub

[Install]
WantedBy=multi-user.target
EOF


sudo systemctl daemon-reload
sudo systemctl enable jupyterhub

useradd -m -s /bin/bash jupyterhub

sudo systemctl start jupyterhub

sudo systemctl status jupyterhub


sudo firewall-cmd --permanent --add-port=8000/tcp
sudo firewall-cmd --reload


screen -S jupyterhub
source /opt/jupyterhub-venv/bin/activate
jupyterhub
Para desconectarte de la sesión de screen sin detener JupyterHub, presiona Ctrl + A seguido de D.
Puedes volver a conectar a la sesión en cualquier momento con:
screen -r jupyterhub



dnf clean all: Elimina todos los archivos almacenados en caché, incluyendo paquetes, metadatos y archivos obsoletos. Esta opción limpia completamente la caché.
dnf clean packages: Elimina los paquetes descargados en la caché, pero conserva los metadatos.
dnf clean metadata: Elimina los archivos de metadatos de los repositorios, como los archivos XML y bases de datos sqlite. Esto fuerza a DNF a descargar nuevos metadatos en la próxima transacción.
dnf clean dbcache: Elimina la caché de datos de los archivos sqlite utilizados para almacenar información de los repositorios.
dnf clean expire-cache: Elimina los paquetes obsoletos de la caché que ya no se utilizan en ningún repositorio habilitado.
dnf clean all --rsh: Elimina los paquetes RPM descargados utilizando el plugin rsh (Remote Source Handle).



docker exec -ti -u root 64eb3bb91845 /bin/bash

docker exec -ti -u root 78b661634ad8 /bin/bash

###instalar vim

apt-get update && apt-get install -y vim

### permisos zeppelin guardar parquet

chmod -R 777 /opt/zeppelin/data


chmod -R 777 /opt/zeppelin/users/dcantorin/salidas/

### comandos dico
df -h
ls -lh
du -sh * 



docker cp bccf6fe902ff:/opt/zeppelin/extranjeros_entrada.parquet /opt/jars_install/
docker cp bccf6fe902ff:/opt/zeppelin/extranjeros_salida.parquet /opt/jars_install/


docker cp e8c590402b1c:/opt/zeppelin/llegadas_LAP.csv /opt/jars_install/
docker cp bccf6fe902ff:/opt/zeppelin/anios_18_34.parquet /opt/jars_install/
docker cp bccf6fe902ff:/opt/zeppelin/anios_35_44.parquet  /opt/jars_install/
docker cp bccf6fe902ff:/opt/zeppelin/anios_45_64.parquet  /opt/jars_install/
docker cp bccf6fe902ff:/opt/zeppelin/anios_65.parquet  /opt/jars_install/

docker cp bccf6fe902ff:/opt/zeppelin/general_salida.parquet  /opt/jars_install/
docker cp bccf6fe902ff:/opt/zeppelin/extranjeros_entrada.parquet  /opt/jars_install/
docker cp bccf6fe902ff:/opt/zeppelin/extranjeros_salida.parquet  /opt/jars_install/

docker cp bccf6fe902ff:/opt/zeppelin/nave_mes  /opt/jars_install/
docker cp bccf6fe902ff:/opt/zeppelin/dias_hora  /opt/jars_install/
docker cp bccf6fe902ff:/opt/zeppelin/dias_hora_2023_salida  /opt/jars_install/
docker cp bccf6fe902ff:/opt/zeppelin/dias_hora_2024_salida  /opt/jars_install/


docker cp bccf6fe902ff:/opt/zeppelin/df_pais_salida  /opt/jars_install/

docker stop bccf6fe902ff 6759c3400179 7af25b4a295f a079901ca1b0 fcd616ed7680


mv df_tiempo_nacionalidad_edad.parquet df_tiempo_nacionalidad_edad_llegada.parquet
docker cp e8c590402b1c:/opt/zeppelin/notebook  /opt/jars_install/


docker cp e8c590402b1c:/opt/zeppelin/horas_llegada  /opt/jars_install/

docker cp /opt/jars_install/dfHorasObs_llegada.parquet e8c590402b1c/opt/zeppelin/data

docker cp e8c590402b1c:/opt/zeppelin/data/richpas/proyectos/analisis_tendencias/output/tpoAtencionModulo_salida_full /opt/jars_install/


docker cp /opt/jars_install/tpoAtencionModulo_llegada_full.parquet 09d268d34b75:/home/richpas/