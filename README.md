*This project has been created as part
of the 42 curriculum by sosanche*


<h1 align="center">Born2beroot
</h1>

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

objetivo
breve descripciń general



## Resources

numera referencias clásicas relacionadas con el tema (documentación, artículos, tutoriales, etc.), así como una descripción de cómo se utilizó la IA.



Lista de cosas para hacer antes de 2030:
- Morir
- Vender mis acciones
- Ser Elon Musk
- Dejar de ser Elon Musk porque te has dado cuenta de que es un puto gillipollas.

1. 1
2. 2

[holas](defitero.com)

![holas](1920x1080.jpg)

<a href="defitero.com"><img src="https://pmecdn.protonweb.com/image-transformation/?s=c&image=image%2Fupload%2Fstatic%2Flogos%2Ficons%2Fmail_xxy4bg.svg"></a>


## Compilation steps
``` bash
make all
```

``` c
#include "libft.h"
// Caca. Eklsdf

int	main(void)
{

}

```

## Additional Sections

1. Debian VS Rocky 

Debian es menos complejo