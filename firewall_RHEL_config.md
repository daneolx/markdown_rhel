En Red Hat Enterprise Linux 8 (RHEL 8), el firewall principal utilizado es `firewalld`. `firewalld` es una utilidad de gestión de firewall dinámico que proporciona una interfaz para administrar reglas de filtrado de paquetes IPv4 e IPv6, así como configuraciones de red de forma más amplia.

Aquí tienes algunos comandos básicos para trabajar con `firewalld` en RHEL 8:

1. **Verificar el estado del firewall:**
   ```bash
   sudo systemctl status firewalld
   ```

2. **Iniciar, detener y reiniciar el servicio firewalld:**
   ```bash
   sudo systemctl start firewalld
   sudo systemctl stop firewalld
   sudo systemctl restart firewalld
   ```

3. **Habilitar o deshabilitar el servicio firewalld para que se inicie automáticamente al arrancar el sistema:**
   ```bash
   sudo systemctl enable firewalld
   sudo systemctl disable firewalld
   ```

4. **Agregar una regla para permitir el tráfico entrante de un puerto específico (por ejemplo, el puerto 80 para HTTP):**
   ```bash
   sudo firewall-cmd --zone=public --add-port=80/tcp --permanent
   sudo firewall-cmd --zone=public --add-port=8088/tcp --permanent
   sudo firewall-cmd --zone=public --add-port=9870/tcp --permanent
   sudo firewall-cmd --zone=public --add-port=8080/tcp --permanent
   sudo firewall-cmd --zone=public --add-port=4040/tcp --permanent
   ```

5. **Recargar las reglas del firewall después de realizar cambios permanentes:**
   ```bash
   
   ```

6. **Listar todas las zonas de firewall:**
   ```bash
   sudo firewall-cmd --get-zones
   ```

7. **Mostrar todas las reglas activas del firewall:**
   ```bash
   sudo firewall-cmd --list-all
   ```

Estos son solo algunos ejemplos básicos de cómo trabajar con `firewalld` en RHEL 8. Puedes encontrar más información en la documentación oficial de Red Hat o mediante la ejecución de `man firewalld` y `man firewall-cmd` en tu terminal.