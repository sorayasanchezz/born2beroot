*This project has been created as part
of the 42 curriculum by sosanche*


<h1 align="center">Born2beroot
</h1>

<img src="https://github.com/mcombeau/mcombeau/raw/main/42_badges/born2beroote.png" style="width:120px;"></a>

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
cat /etc/pam.d/common-password
```

Y para la política de sudo:

``` bash
visudo
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

``` bash 
crontab -e 
```

![result](image.png)

10. Para el bonus la instalación de wordpress es igual para todo el mundo, no es la primera vez que instalaba wordpress así que se me hizo más sencillo que lo demás

11. Lo que entregamos es la firma de la máquina, la cuál cambia cada vez que la abres, por eso es muy importante no tocar la máquina, de hecho lo mejor es quitarte los permisos en ese archivo para que no te deje abrirlo, ya que si no la firma cambia.
Para conseguir la firma hay que ir hacia la carpeta de la máquina virtual

``` bash
shasum machinename.vdi
```

## Resources

[Conceptos clave y organización, contiene los enlaces para descargar VirtualBox y otros necesarios](https://42-fran-byte-f94097.gitlab.io/docs/born2beroot/born2beroot-approach-es/#/)

[Explicaciones, es una página con muchisima información y muy bien hecha](https://www.gibbontech.com/ecole42/born2beroot/index.html)

[Advierte de errores muy útiles como de sgoinfre, var--log y relacionados con contraseña](https://github.com/alx-sch/born2beroot)

[Video de la página anterior](https://www.youtube.com/watch?v=OQEdjt38ZJA&t=349s)

[Mis compañeros me recomendaron esta página cuando me atasqué con la parte de cálculos en el monitoring (ram, almacenamiento y sobretodo CPU)](https://noreply.gitbook.io/born2beroot)

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