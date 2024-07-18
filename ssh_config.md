Para instalar y configurar el servicio SSH en RHEL 8, puedes seguir estos pasos. SSH (Secure Shell) es una herramienta esencial para la administración remota segura de servidores y dispositivos.

### Paso 1: Actualizar el sistema

Primero, asegúrate de que tu sistema esté actualizado:

```bash
sudo dnf update -y
```

### Paso 2: Instalar el servidor SSH

Instala el paquete `openssh-server` usando el siguiente comando:

```bash
sudo dnf install -y openssh-server
```

### Paso 3: Iniciar y habilitar el servicio SSH

Para que el servicio SSH se inicie automáticamente al arrancar el sistema, ejecuta los siguientes comandos:

```bash
sudo systemctl start sshd
sudo systemctl enable sshd
```

### Paso 4: Verificar el estado del servicio SSH

Puedes verificar que el servicio SSH se esté ejecutando correctamente con el siguiente comando:

```bash
sudo systemctl status sshd
```

Deberías ver una salida que indica que el servicio SSH está activo (en ejecución).

### Paso 5: Configuración adicional (opcional)

#### Configurar el cortafuegos para permitir SSH

Asegúrate de que el cortafuegos permita el tráfico SSH. Puedes agregar una regla para permitir el tráfico SSH usando `firewalld`:

```bash
sudo firewall-cmd --permanent --add-service=ssh
sudo firewall-cmd --reload
```

#### Configurar SSH (opcional)

El archivo de configuración de SSH se encuentra en `/etc/ssh/sshd_config`. Puedes editar este archivo para ajustar las configuraciones según tus necesidades. Por ejemplo, para cambiar el puerto SSH o deshabilitar el acceso root:

```bash
sudo nano /etc/ssh/sshd_config
```

- Para cambiar el puerto SSH, busca la línea `#Port 22` y cámbiala a otro puerto, por ejemplo `Port 2222`.
- Para deshabilitar el acceso root, busca la línea `#PermitRootLogin yes` y cámbiala a `PermitRootLogin no`.

Después de hacer cambios en el archivo de configuración, reinicia el servicio SSH para aplicar los cambios:

```bash
sudo systemctl restart sshd
```

### Paso 6: Probar la conexión SSH

Finalmente, prueba la conexión SSH desde otra máquina (cambiando `your_username` y `your_server_ip` por el nombre de usuario y la IP de tu servidor):

```bash
ssh your_username@your_server_ip
```

Si cambiaste el puerto SSH, usa la opción `-p` para especificar el puerto:

```bash
ssh -p 2222 your_username@your_server_ip
```

### Conclusión

Siguiendo estos pasos, habrás instalado y configurado el servicio SSH en tu sistema RHEL 8. Esto te permitirá administrar remotamente tu servidor de manera segura. Asegúrate de revisar y ajustar las configuraciones de SSH según tus necesidades de seguridad y administración.