# Bitácora Prácticas ISE
**-Alumno:** Adrián Varela Jiménez

**-Grupo de prácticas:** C1

**-Usuario:** adriivarela06

**-Curso:** 2026/2027

---

# Práctica 1

  ## Lección 1:
  
  Hemos instalado el sistema operativo ***Debian*** en una máquina virtual, configurando así las particiones y creando una serie de **RAID1** de tal forma que, usando el comando ```lsblk```, vemos que se nos queda el árbol de memoria que tenemos a continuación:
  
  <img width="2560" height="1329" alt="Captura desde 2026-09-24 21-42-29" src="https://github.com/user-attachments/assets/0cb120b5-c5b1-4555-a44c-e66168821c81" />
  
---
  
  ## Lección 2:
  
  En otra máquina virtual, hemos instalado esta vez el sistema operativo ***Alma*** por defecto.
  
  Una vez dentro de nuestra máquina, con la ayuda de comandos de la terminal y scripts de configuración como ```fstab```, hemos conseguido agrandar el tamaño del directorio ```/var```, y usando el comando ```lsblk```, podemos observar que se nos ha quedado el siguiente árbol de memoria:
  
  <img width="2560" height="1329" alt="Captura desde 2026-09-24 21-13-53" src="https://github.com/user-attachments/assets/6fcc66d1-f8ce-4439-a957-77a12d3c167b" />
  
  Una vez establecida nuestra estructura en las memorias de ambas máquinas virtuales, con la ayuda de un un arhivo de configuración de las redes de ambas máquinas, las hemos configurado de tal forma en la que ***Debian*** y ***Alma*** puedan comunicarse entre sí.
  
  Para probarlo hemos hecho un test con el comando ```ping```, probando así que se reciben señales de respuesta por parte de ambas máquinas:
  
  <img width="2557" height="1329" alt="Captura desde 2026-09-24 21-10-25" src="https://github.com/user-attachments/assets/40711117-6f47-4617-8d69-9173c65af537" />
  
---
  
  ## Lección 3:
  
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

  ## Lección 1:

  En esta sesión lo que hemos hecho ha sido configurar el servicio ```ssh``` en las máquinas ***AlmaRaid*** y ***Debian***, así como algunas medidas de seguridad que voy a describir a continuación.

  Al instalar ```ssh``` en ambas máquinas, hemos editado el archivo de configuración ```/etc/ssh/sshd_config``` cambiando así el puerto por defecto al **22022** y prohibiendo el acceso al usuario **root** mediante ```ssh```, aunque en ***Alma*** hemos tenido utilizar un comando que se nos indicaba en este archivo para hacer funcionar el nuevo puerto, además de abrir este puerto en el **firewall** con el comando ```semanage```.

  A continuación hemos ejecutado ell comando ```ssh-keygen``` para crear claves de acceso, y las hemos compartido entre ambas máquinas con el comando ```ssh-copy-id USUARIO@IP -p 22022```, siendo ```USUARIO``` a quien le quieres compartir clave del PC con dirección ```IP```. Esto lo hemos hecho para poder conectar las máquinas sin falta de que estemos poniendo la contraseña cada vez que accedamos.

  <img width="1142" height="772" alt="Captura desde 2026-10-08 17-07-57" src="https://github.com/user-attachments/assets/3226f53e-388e-464e-8898-301b18442cc8" />

  Por último nos hemos descargado ```fail2ban``` para establecer los mecanismos extra de seguridad que he comentado antes. Para aplicar nuesta configuración de seguridad hemos copiado el contenido de  ```/etc/fail2ban/jail.conf``` en ```/etc/fail2ban/jail.local```, y una vez dentro, hemos activado las restricciones de ```ssh``` logrando así que después de un número de intentos de inicio de sesión, se bloquee la IP durante un cierto periodo de tiempo.

  <img width="1920" height="969" alt="Captura desde 2026-10-08 17-15-44" src="https://github.com/user-attachments/assets/4ba4e115-96df-4479-8c20-1518b7867151" />

  ## Lección 2

  En esta sesión hemos creado una ```lamp``` tanto en ***Alma*** como en ***Debian***.

  En ***Debian*** nos hemos instalado ```tasksel```, a través del cual nos hemos podido instalar ```apache2```, y una vez tenemos esto hecho lo único que hay que hacer es arrancar el proceso con ```systemctl start apache2``` y, poniendo nuestra **IP** en nuestro navegador, comprobamos que efectivamente nuestro servidor web está funcionando.

  En ***Alma*** hemos instalado los servicios ```httpd```, ```php```, ```mariadb``` (mysql), y ```mariadb-server``` para poder alojar nuestro servidor en la máquina. Una vez tenemos todo instalado arrancamos los procesos con ```systemctl start nombre_proceso``` y si es necesario los activamos con ```systemctl enable nombre_proceso```.

  Una vez tenemos todos los procesos funcionando, al igual que con ***Debian*** comprobamos en nuestro navegador si tenemos funcionando nuestro servidor web poniendo la **IP** de la máquina.

  A continuación hemos creado el fichero ```/var/www/html/index.php``` para hacer una serie de pruebas en nuestro servidor, y para que se vean los cambios desde el navegador, reiniciamos el servicio ```httpd```.

  <img width="1920" height="969" alt="Captura desde 2026-10-15 16-27-57" src="https://github.com/user-attachments/assets/def1b2d3-262f-44e3-982b-336865ee9669" />

  <img width="1920" height="969" alt="Captura desde 2026-10-15 16-28-05" src="https://github.com/user-attachments/assets/3773e98b-051b-4cf9-9a36-f2de9ddbc064" />

  ## Lección 3
  
  En esta práctica hemos aprendido principalmente a utilizar ```git```, además de ```dd```, ```cp```, ```tar``` y ```rsync``` entre otras utilidades más.
  
  Dentro de la máquina ***Debian*** hemos ido aprendiendo poco a poco las operaciones más importantes de ```git```, como lo son ```git init```, ```git add```, ```git commit``` y ```git status``` entre algunas otras, y a su vez hemos creado,  modificado, y subido a la nube de ```github``` el repositorio ```gta6```.

  Hemos aprendido también a crear nuevas ramas dentro del repositorio con el comando ```git branch <nombre>```, a cambiar de rama con ```git checkout <nombre>```, y a fusionarlas con ```git merge<nombre>```.

  Por último, dejo aquí abajo una imagen con los ```commit``` que he ido haciendo en la clase, véase que he hecho pocos ```commit``` debido a que ya había utilizado ```git``` con anterioridad y me sabía la mayoría de los comandos vistos en la práctica.

  <img width="1920" height="969" alt="Git" src="https://github.com/user-attachments/assets/19edf2a0-efb2-4259-9a36-b7748ca8d64d" />

---

# Práctica 3

  ## Lección 1

  ### Simulación de desconexión y reconexión de una parte del **RAID0** en ***Debian***

  Esta prueba la hemos hecho para simular un accidente hardware que nos podría ocurrir en la vida real, el cual es que nos deje de funcionar uno de los discos de un **RAID0**. 
  
  Provocamos un fallo software en el disco ```/dev/sdb2```, el cual pertenece a nuestro raid ```md1```, con el comando ```sudo mdadm --manage --set-faulty /dev/md1 /dev/sdb2```, y al revisar el archivo ```/proc/mdstat``` podemos comprobar que se nos ha desconectado del raid, por lo que nuestro disco ha quedado expuesto a que si hay otro fallo perdamos todos los datos permanentemente.
  
  Para arreglarlo lo que vamos a hacer es primero eliminar y luego volver a conectar nuestro disco al raid con los comandos ```sudo mdadm -r /dev/md1 /dev/sdb2``` y ```sudo mdadm -a /dev/md1 /dev/sdb2```.

  Por último, para comprobar que ha funcionado el montaje del raid, ejecutamos el comando ```watch -n 1 cat /proc/mdstat``` para ir viendo en tiempo real el porcentaje de los datos que se han copiado de una unidad a otra.

  <img width="2560" height="1329" alt="Captura desde 2026-10-31 18-56-05" src="https://github.com/user-attachments/assets/17c1b991-cfef-4281-bf2c-70ae252e2664" />

  ### Instalación **ZABBIX** ***Debian***

  Para realizar la instalación del servidor **ZABBIX** y su agente en la máquina ***Debian***, lo que vamos a hacer es seguir todos los pasos que se nos indica en su web, teniendo en cuenta que utilizamos la base de datos mysql(mariadb) y servidor apache:
  
    wget https://repo.zabbix.com/zabbix/7.4/release/debian/pool/main/z/zabbix-release/zabbix-release_latest_7.4+debian13_all.deb
    dpkg -i zabbix-release_latest_7.4+debian13_all.deb
    apt update
    
    apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent

    mysql -uroot -p
    password
    mysql> create database zabbix character set utf8mb4 collate utf8mb4_bin;
    mysql> create user zabbix@localhost identified by 'password';
    mysql> grant all privileges on zabbix.* to zabbix@localhost;
    mysql> set global log_bin_trust_function_creators = 1;
    mysql> quit;
    
    zcat /usr/share/zabbix/sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix -p zabbix

    mysql -uroot -p
    password
    mysql> set global log_bin_trust_function_creators = 0;
    mysql> quit;

    Editar archivo /etc/zabbix/zabbix_server.conf:
    DBPassword=practicas,ise
    
    Por último ejecutamos los siguientes comandos:
    systemctl restart zabbix-server zabbix-agent apache2
    systemctl enable zabbix-server zabbix-agent apache2

  <img width="1722" height="1203" alt="Captura desde 2026-11-01 13-28-15" src="https://github.com/user-attachments/assets/f568bf20-f722-4a81-a1ff-aaa198f36f08" />
  <img width="1722" height="1203" alt="Captura desde 2026-11-01 13-28-29" src="https://github.com/user-attachments/assets/3ce37f90-57c1-486c-a814-36c47cc0faca" />

  Una vez tenemos instalado todo, nos metemos desde nuestro navegador y buscamos ```http://192.168.56.105/zabbix```, la cual es la URL de nuestro servidor **ZABBIX**.

  <img width="2560" height="1329" alt="Captura desde 2026-11-01 13-28-58" src="https://github.com/user-attachments/assets/54888cb0-8a9f-4a2b-be88-bc0e52dc3a02" />
  
  Cuando tengamos ya nuestra web iniciada, iniciamos sesion con las credenciales ```Usuario = Admin``` y ```Constraseña = zabbix```, e inmediatamente cambiamos la contraseña para asegurarnos que nadie entre de una forma maliciosa.

  ### Instalación **ZABBIX** ***Alma***

  Ahora, en nuestra máquina ***Alma***, únicamente vamos a instalar el agente de **ZABBIX** de nuevo siguiedo los pasos que se nos indican en la web: 

    Comprobamos la versión de Alma que tenemos con:
    cat /etc/redhat-release
    
    Editamos el archivo /etc/yum.repos.d/epel.repo y añadimos lo siguiente:
    [epel]
    ...
    excludepkgs=zabbix*

    Después ejecutamos los siguientes comandos:    
    rpm -Uvh https://repo.zabbix.com/zabbix/7.4/release/alma/10/noarch/zabbix-release-latest-7.4.el10.noarch.rpm
    dnf clean all

    dnf install zabbix-agent

    systemctl restart zabbix-agent
    systemctl enable zabbix-agent
    
    Una vez que tenemos ZABBIX vamos a configurar en Alma el agente cambiando las siguentes lineas en el archivo /etc/zabbix/zabbix_agentd.conf:
    Server=192.168.56.105
    ServerActive=192.168.56.105
    Hostname=AlmaRaid

    Ahora, como zabbix tiene como puerto predeterminado el 10050, ejecutamos el siguiente comando en ALMA para poder utilizarlo:
    sudo firewall-cmd --add-port=10050/tcp --permanent
    sudo firewall-cmd --reload

  <img width="1320" height="1369" alt="Captura desde 2026-11-01 13-38-47" src="https://github.com/user-attachments/assets/1f840cba-bee9-4a45-a2fe-e1d4aff435b3" />
  
  ### Configuración de la web **ZABBIX**

  Ahora para configurar nuestra web **ZABBIX** y poder monitorear nuestra máquina ***Debian*** y ***Alma***, mientras que para nuestra máquina ***Debian*** no hemos tenido que hacer nada porque ya viene por defecto, para nuestra máquina ***Alma*** la hemos tenido que dar de alta como host poniendo su respectiva IP y el *Puerto 10050*, ya que es el predeterminado que se utiliza para **ZABBIX**, como grupo le ponemos *Linux servers*, y como plantilla *Linux by Zabbix agent*.

  <img width="1920" height="969" alt="Captura desde 2026-11-01 20-25-59" src="https://github.com/user-attachments/assets/12d538b9-1a83-4d2e-902b-41cce687a264" />

  A continuación, para controlar los puertos **SSH** y **HTTP** hemos añadido dos métricas:
  
  Estado del servicio **SSH**: es del tipo comprobación sencilla con clave ```net.wqztcp.service[ssh,,22022]```, dejando ese hueco libre para que se utilice la IP que tenemos por defecto en el host, y ponemos 22022 porque es el puerto que habíamos establecido como predeterminado para este servicio.
  
  Estado del servicio **HTTP**: es del tipo comprobación sencilla y su clave es ```net.tcp.service[http]```, y en este no cambiamos el puerto porque no lo habíamos tocado anteriormente.

  <img width="1210" height="130" alt="Captura desde 2026-11-01 20-27-32" src="https://github.com/user-attachments/assets/549a0c26-be25-4903-b42b-2315a7240aa9" />

  Además también vamos a añadir dos iniciadores para que de un aviso de cuando un servicio se caiga:
  
  Servicio **SSH** caído en AlmaRaid: Expresión ```last(/AlmaRaid/net.tcp.service[ssh,,22022])=0``` y *Severidad Alta*.
  
  Servicio **HTTP** caído en AlmaRaid: Expresión ```last(/AlmaRaid/net.tcp.service[http])=0``` y *Severidad Alta*.

  <img width="1308" height="80" alt="Captura desde 2026-11-01 20-29-25" src="https://github.com/user-attachments/assets/ecd4cb5b-54b0-4fda-91cf-5fd4213b9e17" />
  <img width="1308" height="77" alt="Captura desde 2026-11-01 20-30-29" src="https://github.com/user-attachments/assets/bcc4a2be-cf64-4dbc-b122-92b66d6732d0" />

  ### Simulación de caída del servicio **HTTP**

  Primero comprobamos los últimos valores que tenemos registrados de las conexiones a los servicios **SSH** y **HTTP** para ver que estén ambos funcionando.

  <img width="1920" height="969" alt="Captura desde 2026-11-01 20-33-09" src="https://github.com/user-attachments/assets/4c407d95-3680-4a45-9fa0-12d78895ec09" />

  <img width="1920" height="969" alt="Captura desde 2026-11-01 20-33-17" src="https://github.com/user-attachments/assets/4714dca3-e715-4247-8c77-dd4aae73df54" />

  A continuación apagamos el servicio **HTTP** con el comando ```sudo systemctl stop httpd``` para simular la caída, y comprobamos en nuestro panel principal de la web **ZABBIX** que nos ha saltado el error.

  <img width="1920" height="969" alt="Captura desde 2026-11-01 20-36-07" src="https://github.com/user-attachments/assets/ec256693-4f0b-4bd3-bac3-cb6b8728ab68" />

  Por último encendemos de nuevo el servicio con el comando ```sudo systemctl start httpd``` y comprobamos que en nuestro panel se ha quitado la alerta del fallo y nos sale como resuelto.

  <img width="1920" height="969" alt="Captura desde 2026-11-01 20-38-13" src="https://github.com/user-attachments/assets/ed03d57e-f5f6-4af6-a818-c1f844bc1c64" />

  ### Problemas que me han surgido por el camino

  Al instalar el agente en ***Alma***, hemos tenido que modificar el archivo ```/etc/zabbix/zabbix_agentd.conf``` para establecer como servidor de **ZABBIX** predeterminado el de nuestra máquina ***Debian***.

  En la métrica **SSH**, al poner ```net.tcp.service[ssh]``` y probarla nos daba error, por lo que tuvimos que modificarla añadiendo el puerto que habíamos cambiado por defecto quedándose así: ```net.tcp.service[ssh,,22022]```.

  Al configurar el agente **ZABBIX**, nos hemos topado con que el puerto 10050 no funcionaba (puerto por defecto de **ZABBIX**), por lo que hemos tenido que abrir en el firewall para que pueda comunicarse con el agente y viceversa.

  ## Lección 2

  En esta lección, hemos aprendido como levantar un servicio de monitorización de discos RAID automatizado localmente en ***Debian***, y la configuración de ```ansible``` para ejecutar tareas remotas en ***AlmaRaid***.

  Para automatizar la revisión del estado de nuestros RAIDs sin depender de ```cron```, se nos han dado tres ficheros llamados ```mon_raid```, uno con extensión *.py*, otro con *.service*, y otro con *.timer*, los cuales he enviado a la máquina ***Debian*** haciendo uso del servicio ```scp /ruta/local/archivo usuario@ip_remota:/ruta/destino/```.
  
Una vez que ya tenemos los archivos en nuestra máquina ***Debian***, usando la herramienta ```systemctl```, habilitamos primero nuestro ```mon_raid.timer```, el cual es el trigger de ```mon_raid.system```, con el comando ```sudo systemctl enable mon_raid.timer```. Por último habilitamos y arrancamos nuestro sistema ```mon_raid.system```, el cual nos ejecuta el fichero ```mon_raid.py```, con los comandos ```sudo systemctl enable mon_raid``` y ```sudo systemctl start mon_raid```.

Ahora, para ver que todo está funcionando correctamente ejecutamos ```sudo systemctl status mon_raid.timer``` y ```sudo systemctl status mon_raid.timer```, y después, para ver si se ha ejecutado nuestro servicio y sus salidas, ejecutamos ```sudo journaltrl -u mon_raid```.

<img width="1920" height="969" alt="Captura desde 2026-11-05 16-07-25" src="https://github.com/user-attachments/assets/a27461af-9188-4fe6-9197-94d5f22fbc19" />
<img width="1762" height="939" alt="Captura desde 2026-11-08 20-20-30" src="https://github.com/user-attachments/assets/acfac4b8-0a0e-4a04-a5b0-28dce0f5aacd" />

A continuación, hemos instalado el servicio ```ansible```, el cual sirve para ejecutar comandos en varias máquinas al mismo tiempo desde solamente una. Inmediatamente ejecutamos el comando ```sudo ansible-config init >> /etc/ansible/ansible.conf``` para poder modificar los parámetros del servicio a nuestro gusto dentro de su archivo de configuración.

Después, hemos creado un fichero ```hosts``` con las IPs de las máquinas en las que queremos ejecutar los comandos, siendo estas IPs las de ***Debian*** y ***AlmaRaid***. Una vez que tenemos nuestro fichero, para que funcione el comando ```ansible``` hemos tenido que exportar desde la máquina ***Debian*** a si misma su clave pública de **SSH**, y la de ***AlmaRaid*** no ha hecho falta porque ya la habíamos exportado en una lección anterior.

Una vez tenemos todo configurado, hemos probado que funcionara con ```ansible -i hosts all -m ping```, y hemos pasado con ```scp``` el archivo ```mon_raid.py``` a la máquina ***AlmaRaid*** para poder ejecutarlo de forma remota. Por último, hemos ejecutado ```ansible -i hosts all -a "/home/adrian/mon_raid.py"``` y comprobado que los resultados son los que esperamos.

<img width="1762" height="939" alt="Captura desde 2026-11-08 12-55-21" src="https://github.com/user-attachments/assets/e3385fa1-a0f8-4a94-8c02-e3d878896222" />
