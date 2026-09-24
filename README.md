# Bitácora Prácticas ISE
**-Alumno:** Adrián Varela Jimènez

**-Grupo de prácticas:** C1

**-Usuario:** adriivarela06

**-Curso:** 2026/2027

---

## Sesión 1:

Hemos instalado el sistema operativo ***Debian*** en una máquina virtual, configurando así las particiones de tal forma que, usando el comando **lsblk**, vemos que se nos queda el árbol de memoria que tenemos a continuación:

<img width="2560" height="1329" alt="Captura desde 2026-09-24 21-42-29" src="https://github.com/user-attachments/assets/0cb120b5-c5b1-4555-a44c-e66168821c81" />

---

## Sesión 2:

En otra máquina virtual, hemos instalado esta vez el sistema operativo ***Alma*** por defecto.

Una vez dentro de nuestra máquina, con la ayuda de comandos de la terminal y scripts de configuración como **fstab**, hemos conseguido agrandar el tamaño del directorio **/var**, y usando el comando **lsblk**, podemos observar que se nos ha quedado el siguiente árbol de memoria:

<img width="2560" height="1329" alt="Captura desde 2026-09-24 21-13-53" src="https://github.com/user-attachments/assets/6fcc66d1-f8ce-4439-a957-77a12d3c167b" />

Una vez establecida nuestra estructura en las memorias de ambas máquinas virtuales, con la ayuda de un un arhivo de configuración de las redes de ambas máquinas, las hemos configurado de tal forma en la que ***Debian*** y ***Alma*** puedan comunicarse entre sí.

Para probarlo hemos hecho un test con el comando **ping**, probando así que se reciben señales de respuesta por parte de ambas máquinas:

<img width="2557" height="1329" alt="Captura desde 2026-09-24 21-10-25" src="https://github.com/user-attachments/assets/40711117-6f47-4617-8d69-9173c65af537" />
