+++
date = 2024-07-03
title = "HTB Dancing WriteUp"
slug = ""
author = ["R4NC0X"]
description = "HackThebox 'Dancing' WriteUp"
draft = false
tags = [
    "HTB",
    "Maquina",
    "Windows",
    "Protocolos",
    "Smb",
    "Reconocimiento",
    "Acceso anonimo/invitados",
]
+++

# Dancing -- HacktheBox

- Sistema: _Windows_
- Dificultad: _Muy Facil_
- Plataforma: _HacktheBox_

!['Dancing' Avatar](/images/Dancing/Dancing.png)

___

## Resumen 

"Dancing" es una maquina de dificultad "Muy Facil" de la plataforma `HackTheBox`. Dancing forma parte de los laboratorios de `Punto de Partida`.

Para completar la maquina ejecute nmap para realizar un escaneo de puertos a la dirrecion ip `10.129.22.109`, la maquina nos propone el uso de un servicio que es `SMB` [Server Message Block] entonces supe que mi escaneo tendria que enfocarse en el puerto `445`. Ya que supe que servicio esta abierto usando el comando `smbclient -L [DireccionIp]` liste las Acciones de la maquina y procedi a tratar de ingresar en cada una de ellas con el comando `smbclient -N \\\\10.129.22.109\\[Sharename]`, la unica accion a la que pude ingresar sin contraseña fue `WorkShares`. Ya dentro listo con `dir` los contenidos y encuentro que hay dos directorios `Amy.J` y `James.P` ingreso al directorio de `Amy.J` usando el comando `cd` procedi a revisar sus contenidos y no encontre la flag por lo que regrese al directorio principal usando `cd ..` y procedi a ingresar al directorio `James.P` haciendo `dir` encuentro un archivo `flag.txt`, usando el comando `more flag.txt` listo el contenido encontrando la bandera y resolviendo la maquina. 

___

## Procedimiento

Comence resolviendo las Tareas de la maquina, algunas de las tareas son pistas para resolver las maquina.

- **Tarea 1 ¿Qué significa el acrónimo de tres letras SMB?**

`bloque de mensajes del servidor`

- **Tarea 2 ¿En qué puerto opera SMB?**

`445`

- **Tarea 3 ¿Cuál es el nombre del servicio para el puerto 445 que apareció en nuestro escaneo de Nmap?**

`microsoft-ds`

- **Tarea 4 ¿Cuál es la 'bandera' o 'interruptor' que podemos usar con la utilidad smbclient para 'enumerar' las acciones disponibles en Dancing?**

`-L`

- **Tarea 5 ¿Cuántas acciones hay en Dancing?**

`4`

- **Tarea 6 ¿Cuál es el nombre del recurso compartido al que finalmente podemos acceder con una contraseña en blanco?**

`WorkShares`

- **Tarea 7 ¿Cuál es el comando que podemos usar dentro del shell de SMB para descargar los archivos que encontremos?**

`get`

- **Enviar Bandera Root**

Para encontrar la bandera realice un escaneo de puertos a la direccion ip de la maquina usando la herramienta `nmap`.

![Anexo1](/images/Dancing/Anexo1.png)

Como realice el escaneo al puerto `445` de la maquina solo me muestra los datos del servicio `microsoft-ds`. 

![Anexo2](/images/Dancing/Anexo2.png)

Usando el comando `smbclient -L [DireccionIp]` listo todas las Acciones de la maquina para ver en cual de las 4 que se muestran se puede acceder sin contraseña.

![Anexo3](/images/Dancing/Anexo3.png)

Ya que encontre la Accion que me permite ingresar sin contraseña use el comando `smbclient -N \\\\10.129.22.109\\WorkShares`.

![Anexo4](/images/Dancing/Anexo4.png)

Ya adentro procedo a listar todos los contenidos del directorio principal con el comando `dir` encontrando que hay dos directorios.

``` bash
smb: \> dir
  .                                   D        0  Mon Mar 29 03:22:01 2021
  ..                                  D        0  Mon Mar 29 03:22:01 2021
  Amy.J                               D        0  Mon Mar 29 04:08:24 2021
  James.P                             D        0  Thu Jun  3 03:38:03 2021

		5114111 blocks of size 4096. 1753536 blocks available
smb: \> 

```
Primero ingreso al directorio `Amy.J` con el comando `cd` y procedo a listar todos los contenidos que se encuentran en el.

``` bash
smb: \> cd Amy.J
smb: \Amy.J\> dir
  .                                   D        0  Mon Mar 29 04:08:24 2021
  ..                                  D        0  Mon Mar 29 04:08:24 2021
  worknotes.txt                       A       94  Fri Mar 26 06:00:37 2021

		5114111 blocks of size 4096. 1753520 blocks available
smb: \Amy.J\> 

```
Encuentro un archivo llamado `worknotes.txt` y con el comando `more` listo el contenido del archivo.

``` bash
- start apache server on the linux machine
- secure the ftp server
- setup winrm on dancing 

```
El archivo `worknotes.txt` no contenia la bandera de esta maquina por lo que con el comando `cd ..` regreso al directorio principal y posterior ingreso al directorio `James.P` y listo los contenidos de ese directorio.

``` bash
getting file \Amy.J\worknotes.txt of size 94 as /tmp/smbmore.Sda4KS (0.0 KiloBytes/sec) (average 0.0 KiloBytes/sec)
smb: \Amy.J\> cd ..
smb: \> cd James.P
smb: \James.P\> dir
  .                                   D        0  Thu Jun  3 03:38:03 2021
  ..                                  D        0  Thu Jun  3 03:38:03 2021
  flag.txt                            A       32  Mon Mar 29 04:26:57 2021

		5114111 blocks of size 4096. 1753646 blocks available
smb: \James.P\> 

```
Observe que hay un archivo llamado `flag.txt` por lo que no dude en ver su contenido para encontrar la bandera.

``` bash
5f61c10dffbc77a704d76016a2******

```
Ingreso la bandera en la ultima Tarea de la maquina `Enviar bandera`.

Una ves enviada la bandera salio un mensaje diciendo `Dancing has been Pwned`.

![Anexo5](/images/Dancing/Anexo5.png)
___

## Maquina Completada :)



