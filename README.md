*This project has been created as part
of the 42 curriculum by sosanche*


<h1 align="center">Born2beroot
</h1>

<a href="defitero.com"><img src="https://media.eu.badgr.com/uploads/issuers/issuer_logo_3b392490-eb21-4e1a-a068-d0df9f079c8b.png"></a>

## Description

Este proyecto trata sobre crear un servidor minimalista en una máquina virtual aplicando algunas reglas como por ejemplo controlar particiones cifradas, creación de usuarios y grupos, script de monitorización en bash y instalación de servicios como WordPress, ssh, firewall.. 

## Instructions

1. Escoger que versión escoges, yo elegí debian y no rocky porque era la opción más fácil y yo no me manejo mucho con máquinas virtuales, esta tienes que descargarla sin entorno gráfico

2. Durante la instalación configuré las particiones cifradas con LVM que aparecen predeterminadas y luego cree otras dos aparte

``` bash
lsblk
```

3. Llamo a mi hostname sosache42, como bien pide el ejercicio

``` bash
hostnamectl
```

4. Compruebas que AppArmor está activado

``` bash
sudo systemctl apparmor
```

5. Creo el primer usuario que es sosanche, al crearlo está en el grupo sosanche42 y también agrego este usuario al grupo user

``` bash
sudo adduser <user>
sudo addgorup <user>
sudo usermod -aG group user
groups <user>
```

6. Para instalar ssh marqué la opcion inicial en la parte de instalación, por seguridad para prevenir ataques en el pruerto predefinido en la configuración sshd_config escribí el puerto 4242 y en port forwarding puse que el puerto 2222 lleve al 4242.

7. Instalé el firewall para debian ufw, desactivé todos los puertos menos los que he usado, por ejemplo para ssh con el comando ufw allow 4242 

``` bash
sudo ufw enable
sudo ufw status
```

8. Para la politica estricta de contraseñas utilicé:

``` bash
sudo chage -l <user>
cat /etc/login.defs
cat /etc/padm.d/common-password
```

Y para la política de sudo:

``` bash
cat /var/log/sudo/
```

9. Después cree el monitoring, el cual utilicé cron para que aparezca cada 10 minutos:

- arquitectura del sistema
- número de CPUs físicas y virtuales
- RAM libre y % usado
- almacenamiento libre y % usado
- carga de CPU
- último reinicio
- si LVM está activo
- conexiones activas
- usuarios logueados
- IP + MAC
- número de comandos sudo ejecutados


explicar la elección del sistema operativo (Debian o Rocky), con sus respectivas ventajas y desventajas

Debe indicar las principales decisiones de diseño tomadas durante la configuración (particionamiento, políticas de seguridad, administración de usuarios, servicios instalados), así como una comparación entre:
◦ Debian vs. Rocky Linux
◦ AppArmor vs. SELinux
◦ UFW vs. Firewalld
◦ VirtualBox vs. UTM

## Resources

numera referencias clásicas relacionadas con el tema (documentación, artículos, tutoriales, etc.), así como una descripción de cómo se utilizó la IA.

[holas](defitero.com)

![holas](1920x1080.jpg)




## Additional Sections

1. Debian VS Rocky 

Elegí debian y no rocky porque es más sencillo de instalar, y estaba más o menos familiarizada con los comandos, la instalación es más guiada, rocky linux está pensado más para entornos empresariales, más para ser un servidor. Debian tiene menos opciones/capas de seguridad que tocar, es menos técnico y te recomiendan usar Rocky Linux si tienes experiencia de antes con máquinas virtuales.

2. AppArmor vs SELinux

AppArmor controla qué puede hacer un programa según la ruta del archivo, por ejemplo, si el programa está en /mono/banana, solo puede acceder a archivos que haya dentro de /mono/banana, por ejemplo no podría entrar a /mono/cocodrilo, esto se hace por seguridad para que no puedan modificar o leer archivos que no corresponden.

SElinux funciona de manera similar pero no con la ruta, si no con etiquetas, ya que todos los archivos, procesos.. tienen una etiqueta de seguridad, por ejemplo httpd_t puede interactuar con httpd_sys_content_t y es más estricto, ya que si un proceso tiene una etiqueta mal puesta, el proceso muere.

3. UFW vs firewalld

Cambia bastante en dificultad, UFW está bastante humanizado, esto lo voy a explicar con el ejemplo de SSH, en UFW tardas dos segundos, en firewalld para entender lo que estás haciendo tardas mucho más:

UFW:
``` bash
sudo ufw allow OpenSSH
sudo ufw allow 22
```

firewalld:
``` bash
sudo firewall-cmd --zone=public --add-service=ssh --permanent
sudo firewall-cmd --reload
```

4. VirtualBox vs UTM

La diferencia es según la estructura de procesador que tengas, VirtualBox sirve para x86_64 (Intel, AMD), y UTM funciona en procesadores ARM, sirve mayormente para MAC, porque en Linux y Windows no vas a tener esos procesadores.

