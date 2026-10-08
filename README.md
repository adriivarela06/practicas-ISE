# Bitácora Prácticas ISE
**-Alumno:** Adrián Varela Jiménez

**-Grupo de prácticas:** C1

**-Usuario:** adriivarela06

**-Curso:** 2026/2027

---

# Práctica 1

  ## Sesión 1:
  
  Hemos instalado el sistema operativo ***Debian*** en una máquina virtual, configurando así las particiones y creando una serie de **RAID1** de tal forma que, usando el comando ```lsblk```, vemos que se nos queda el árbol de memoria que tenemos a continuación:
  
  <img width="2560" height="1329" alt="Captura desde 2026-09-24 21-42-29" src="https://github.com/user-attachments/assets/0cb120b5-c5b1-4555-a44c-e66168821c81" />
  
---
  
  ## Sesión 2:
  
  En otra máquina virtual, hemos instalado esta vez el sistema operativo ***Alma*** por defecto.
  
  Una vez dentro de nuestra máquina, con la ayuda de comandos de la terminal y scripts de configuración como ```fstab```, hemos conseguido agrandar el tamaño del directorio ```/var```, y usando el comando ```lsblk```, podemos observar que se nos ha quedado el siguiente árbol de memoria:
  
  <img width="2560" height="1329" alt="Captura desde 2026-09-24 21-13-53" src="https://github.com/user-attachments/assets/6fcc66d1-f8ce-4439-a957-77a12d3c167b" />
  
  Una vez establecida nuestra estructura en las memorias de ambas máquinas virtuales, con la ayuda de un un arhivo de configuración de las redes de ambas máquinas, las hemos configurado de tal forma en la que ***Debian*** y ***Alma*** puedan comunicarse entre sí.
  
  Para probarlo hemos hecho un test con el comando ```ping```, probando así que se reciben señales de respuesta por parte de ambas máquinas:
  
  <img width="2557" height="1329" alt="Captura desde 2026-09-24 21-10-25" src="https://github.com/user-attachments/assets/40711117-6f47-4617-8d69-9173c65af537" />
  
---
  
  ## Sesión 3:
  
  Al igual que en la sesión 3, hemos creado una nueva máquina virtual nueva con la instalación del sistema operativo ***Alma*** por defecto.
  
  Esta vez nuestro objetivo era hacer lo mismo que en la sesión anterior, es decir, agrandar el tamaño del directorio ```/var``` utilizando un **RAID1** y además cifrandolo.
  
  Para ello hemos ejecutado todos estos comandos en la terminal, los cuáles vemos utilizando el comando ```history```:
  
  <img width="1920" height="969" alt="Captura desde 2026-10-01 17-15-56" src="https://github.com/user-attachments/assets/5ae2c524-70e3-4807-b382-4b65d5cfe4b4" />
  
  <img width="1920" height="969" alt="Captura desde 2026-10-01 17-16-10" src="https://github.com/user-attachments/assets/3763edee-9683-457b-b984-d7acae97a60f" />
  
  <img width="1920" height="969" alt="Captura desde 2026-10-01 17-16-24" src="https://github.com/user-attachments/assets/1a4bee10-9d81-443d-b27c-4e260655c24d" />
  
  <img width="1920" height="969" alt="Captura desde 2026-10-01 17-17-12" src="https://github.com/user-attachments/assets/26a6f029-fb17-4977-9030-ba35c626b4fa" />
  
  Además, también hemos modificado el archivo ```fstab```, para que el punto de montaje de nuestro **RAID1** sea en ```/var```, y también el archivo ```crypttab``` para que cuando iniciemos la máquina se nos pida la clave de desencriptado, teniendo así nuestra carpeta ```/var``` lista para su uso al encender la máquina. 
  
  Si no hiciéramos esto, cada vez que encendieramos la máquina tendriamos que hacer el comando ```cryptsetup luksOpen /dev/mapper/vgraid-newvar vgraid-newvar_open```
  
  Una vez que tenemos todo hecho, comprobamos que el árbol de memoria se ha quedado como nosotros queríamos viéndolo con el comando ```lsblk```:
  
  <img width="1920" height="969" alt="Captura desde 2026-10-01 17-17-46" src="https://github.com/user-attachments/assets/23945c4c-9413-4f56-b9dc-0a79504f66ff" />

---

# Práctica 2

  ## Sesión 1:

  En esta sesión lo que hemos hecho ha sido configurar el servicio ```ssh``` en las máquinas ***AlmaRaid*** y ***Debian***, así como algunas medidas de seguridad que voy a describir a continuación.

  Al instalar ```ssh``` en ambas máquinas, hemos editado el archivo de configuración ```/etc/ssh/sshd_config``` cambiando así el puerto por defecto al **22022** y prohibiendo el acceso al usuario **root** mediante ```ssh```, aunque en ***Alma*** hemos tenido utilizar un comando que se nos indicaba en este archivo para hacer funcionar el nuevo puerto, además de abrir este puerto en el **firewall** con el comando ```semanage```.

  A continuación hemos ejecutado ell comando ```ssh-keygen``` para crear claves de acceso, y las hemos compartido entre ambas máquinas con el comando ```ssh-copy-id USUARIO@IP -p 22022```, siendo ```USUARIO``` a quien le quieres compartir clave del PC con dirección ```IP```. Esto lo hemos hecho para poder conectar las máquinas sin falta de que estemos poniendo la contraseña cada vez que accedamos.

<img width="1142" height="772" alt="Captura desde 2026-10-08 17-07-57" src="https://github.com/user-attachments/assets/3226f53e-388e-464e-8898-301b18442cc8" />

Por último nos hemos descargado ```fail2ban``` para establecer los mecanismos extra de seguridad que he comentado antes. Para aplicar nuesta configuración de seguridad hemos copiado el contenido de  ```/etc/fail2ban/jail.conf``` en ```/etc/fail2ban/jail.local```, y una vez dentro, hemos activado las restricciones de ```ssh``` logrando así que después de un número de intentos de inicio de sesión, se bloquee la IP durante un cierto periodo de tiempo.

<img width="1920" height="969" alt="Captura desde 2026-10-08 17-15-44" src="https://github.com/user-attachments/assets/4ba4e115-96df-4479-8c20-1518b7867151" />

