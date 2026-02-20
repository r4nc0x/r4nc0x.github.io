+++
date = 2024-07-02
title = "HTB Fawn WriteUp"
slug = ""
author = ["R4NC0X"]
description = "HackThebox 'Fawn' WriteUp"
draft = false
tags = [
    "HTB",
    "Maquina",
    "Linux",
    "Ftp",
    "Protocolos",
    "Reconocimiento",
    "Acceso anonimo/invitados",
]
+++

# Fawn -- HacktheBox

- Sistema: _Linux_
- Dificultad: _Muy Facil_
- Plataforma: _HacktheBox_

!['Fawn' Avatar](/images/Fawn/Fawn.webp)

___

## Resumen 

"Fawn" es una maquina de dificultad "Muy Facil" de la plataforma `HackTheBox`. Fawn forma parte de los laboratorios de `Punto de Partida`.

Para completar esta maquina ejecute nmap para realizar un escaneo de puertos a la dirrecion ip `10.129.219.195`, la maquina Fawn trata del protocolo "FTP" por lo que mi escaneo a la maquina dio como resultado un puerto abierto 21/TCP ya que sabia que se trata de un puerto FTP use el comando `ftp [DireccionIp]` me conecto a la maquina con un nombre predeterminado `anonymous` y con una contraseña en blanco ingreso a la maquina, dentro de la maquina ejecuto el comando `ls` para listar los contenidos, el resultado de la busqueda me arroja un archivo `flag.txt` y con el comando `get` me dascargo el archivo en mi maquina, hago un `cat flag.txt` y asi consigo la bandera de la maquina Fawn

___

## Procedimiento

Empezamos resolviendo las Tareas de la maquina, algunas de las tareas son pistas para resolver la maquina. 

- **Tarea 1 ¿Qué significa el acrónimo de 3 letras FTP?** 

`Protocolo de Transferencia de Archivos`

- **Tarea 2 ¿En qué puerto escucha habitualmente el servicio FTP?**

`21`

- **Tarea 3 ¿Qué acrónimo se utiliza para la versión de FTP protegida mediante la ejecución del protocolo SSH?**

`sftp`

- **Tarea 4 ¿Cuál es el comando que podemos usar para enviar una solicitud de eco ICMP para probar nuestra conexión con el objetivo?**

`Ping`

- **Tarea 5 Según sus escaneos, ¿qué versión de FTP se ejecuta en el destino?**

`vsftpd 3.0.3`

- **Tarea 6 Según sus análisis, ¿qué tipo de sistema operativo se ejecuta en el objetivo?**

`Unix`

- **Tarea 7 ¿Cuál es el comando que debemos ejecutar para mostrar el menú de ayuda del cliente 'ftp'?**

`ftp -h`

- **Tarea 8 ¿Cuál es el nombre de usuario que se utiliza en FTP cuando desea iniciar sesión sin tener una cuenta?**

`Anonymous`

- **Tarea 9 ¿Cuál es el código de respuesta que recibimos para el mensaje FTP 'Inicio de sesión exitoso'?**

`230`

- **Tarea 10 Hay un par de comandos que podemos usar para enumerar los archivos y directorios disponibles en el servidor FTP. Uno es dir. ¿Cuál es la otra forma común de enumerar archivos en un sistema Linux?**

`ls`

- **Tarea 11 ¿Cuál es el comando utilizado para descargar el archivo que encontramos en el servidor FTP?**

`get`

- **Enviar Bandera Root**

Para poder encontrar la bandera realice un escaneo a la ip de la maquina usando la herramienta `Nmap`.

![Anexo1](/images/Fawn/Anexo1.png)

Observe que hay un unico puerto abierto `21/tcp`, es un servicio `FTP`, el escaneo tambien nos muestra datos importantes como la version, login, y permisos. 

![Anexo2](/images/Fawn/Anexo2.png)

Usando el comando `ftp [DireccionIp]` ingreso y me pide un nombre de usuario, ftp proporciona un usuario por defecto, por lo que usando el nombre `anonymous` y con una contraseña vacia logro ingresar a la maquina. 

![Anexo3](/images/Fawn/Anexo3.png)

Ya dentro de la maquina use `ls` para listar contenidos y observe que hay un archivo llamado `flag.txt` con el comando `get` me descargo en mi maquina.

``` bash
ftp> ls
229 Entering Extended Passive Mode (|||9137|)
150 Here comes the directory listing.
-rw-r--r--    1 0        0              32 Jun 04  2021 flag.txt
226 Directory send OK.
ftp> get flag.txt
local: flag.txt remote: flag.txt
229 Entering Extended Passive Mode (|||39526|)
150 Opening BINARY mode data connection for flag.txt (32 bytes).
100% |*************************************************************************************************************************************************************************************************|    32       21.25 KiB/s    00:00 ETA
226 Transfer complete.
32 bytes received in 00:00 (0.14 KiB/s)
```
En mi maquina con el comando `cat` descubro la flag.

``` bash
❯ cat flag.txt
───────┬──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: flag.txt
───────┼──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ 035db21c88152006**************

```
Ingreso la flag en la ultima Tarea de la maquina `Enviar bandera`.

Una ves enviada la bandera salio un mensaje diciendo `Fawn has been Pwned`.

![Anexo4](/images/Fawn/Anexo4.png)
___

## Maquina Completada :)



