# Bitácora Prácticas ISE
**-Alumno:** Adrián Varela Jiménez

**-Grupo de prácticas:** C1

**-Usuario:** adriivarela06

**-Curso:** 2026/2027

---

## Sesión 1:

Hemos instalado el sistema operativo ***Debian*** en una máquina virtual, configurando así las particiones de tal forma que, usando el comando ```lsblk```, vemos que se nos queda el árbol de memoria que tenemos a continuación:

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

Esta vez nuestro objetivo era hacer lo mismo que en la sesión anterior, es decir, agrandar el tamaño del directorio ```/var``` utilizando un volumen físico, pero esta vez, además de esto vamos a cifrarlo.

Para ello hemos ejecutado todos estos comandos en la terminal, los cuáles vemos utilizando el comando ```history```:

<img width="1920" height="969" alt="Captura desde 2026-10-01 17-15-56" src="https://github.com/user-attachments/assets/5ae2c524-70e3-4807-b382-4b65d5cfe4b4" />

<img width="1920" height="969" alt="Captura desde 2026-10-01 17-16-10" src="https://github.com/user-attachments/assets/3763edee-9683-457b-b984-d7acae97a60f" />

<img width="1920" height="969" alt="Captura desde 2026-10-01 17-16-24" src="https://github.com/user-attachments/assets/1a4bee10-9d81-443d-b27c-4e260655c24d" />

<img width="1920" height="969" alt="Captura desde 2026-10-01 17-17-12" src="https://github.com/user-attachments/assets/26a6f029-fb17-4977-9030-ba35c626b4fa" />

Además, también hemos modificado el archivo ```fstab```, para que el punto de montaje de nuestro nuevo volumen físico sea en ```/var```, y también el archivo ```crypttab``` para que cuando iniciemos la máquina se nos pida la clave de desencriptado, teniendo así nuestra carpeta ```/var``` lista para su uso al encender la máquina. 

Si no hiciéramos esto, cada vez que encendieramos la máquina tendriamos que hacer el comando ```cryptsetup luksOpen /dev/mapper/vgraid-newvar vgraid-newvar_open```

Una vez que tenemos todo hecho, comprobamos que el árbol de memoria se ha quedado como nosotros queríamos viéndolo con el comando ```lsblk```:

<img width="1920" height="969" alt="Captura desde 2026-10-01 17-17-46" src="https://github.com/user-attachments/assets/23945c4c-9413-4f56-b9dc-0a79504f66ff" />
