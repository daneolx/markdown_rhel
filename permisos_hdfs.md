En Hadoop, ajustar los propietarios de directorios y archivos puede ser un poco diferente a los sistemas de archivos convencionales. Aquí te explico cómo puedes hacerlo:

### Cambiar el Propietario y Grupo en Hadoop

Para cambiar el propietario y grupo de un directorio en Hadoop, puedes usar el comando `hadoop fs -chown` seguido del nuevo propietario y grupo especificados. Aquí está la sintaxis general:

```bash
hadoop fs -chown [-R] <nuevo_propietario>[:<nuevo_grupo>] <ruta_del_directorio_o_archivo>
```

- `-R`: Opción para cambiar recursivamente el propietario y grupo de todos los archivos y subdirectorios dentro del directorio especificado.

#### Ejemplos de Uso

1. **Cambiar solo el propietario:**
   
   ```bash
   hadoop fs -chown dcantorin /user/data/raw/SIM
   ```

   Esto cambiará el propietario del directorio `/user/data/raw/SIM` a `dcantorin`, manteniendo el grupo actual.

2. **Cambiar propietario y grupo:**
   
   ```bash
   hadoop fs -chown dcantorin:supergroup /user/data/raw/SIM
   ```

   Esto cambiará tanto el propietario como el grupo del directorio `/user/data/raw/SIM` a `dcantorin` y `supergroup`, respectivamente.

3. **Cambiar recursivamente (para todos los archivos y subdirectorios):**
   
   ```bash
   hadoop fs -chown -R dcantorin:supergroup /user/data/raw
   ```

   Esto cambiará de manera recursiva el propietario y grupo de todos los archivos y subdirectorios bajo `/user/data/raw` a `dcantorin` y `supergroup`.

### Consideraciones

- **Permisos**: Después de cambiar el propietario y grupo, asegúrate de que los permisos sean adecuados para que los usuarios y grupos necesarios puedan acceder al directorio según sea necesario (`chmod` se utiliza para ajustar los permisos en Hadoop).

- **Configuración de Seguridad**: Asegúrate de tener los permisos necesarios para ejecutar estos comandos y de que tu usuario tenga los privilegios adecuados en Hadoop para realizar cambios de propietario.

Siguiendo estos pasos, deberías poder ajustar los propietarios y grupos de los directorios y archivos en Hadoop según tus necesidades específicas.