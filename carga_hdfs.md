# Verificar el archivo en el sistema local
ls /home/user/data/archivo.parquet

# Subir el archivo a HDFS
hdfs dfs -put /home/user/data/archivo.parquet /user/hadoop/data/

# Verificar la carga del archivo en HDFS
hdfs dfs -ls /user/hadoop/data/


/user/data/raw

# Permisos  por usuario
hdfs dfs -chmod -R 777 /user/richpas

# Alternativamente, cambiar el propietario del directorio a dcantorin:
hdfs dfs -chown -R lvilchez:supergroup /user/lvilchez

# Conceder permisos de escritura al usuario `dcantorin`
hdfs dfs -chmod -R 777 /user/ssosa

# Verificar los permisos
hdfs dfs -ls /user/ltaipe


hdfs dfs -put /opt/jars_install/df_Flight /user/data/raw/ATSG/


hdfs dfs -chown -R dcantorin:supergroup /data/raw/SIM/movmigra_anual/

hdfs dfs -chmod -R 777 /data/raw/SIM/movmigra_anual/