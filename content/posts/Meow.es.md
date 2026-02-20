+++
date = 2024-06-27
title = "HTB Meow WriteUp"
slug = ""
author = ["R4NC0X"]
description = "HackThebox 'Meow' WriteUp"
draft = false
tags = [
    "HTB",
    "Maquina",
    "Linux",
    "Telnet",
    "Protocolos",
    "Reconocimiento",
    "Credenciales Debiles",
    "Mala Configuracion",
]
+++

# Meow -- HacktheBox

- Sistema: _Linux_
- Dificultad: _Muy Facil_
- Plataforma: _HacktheBox_

!['Meow' Avatar](/images/Meow/Meow.webp)

___

## Resumen 

"Meow" es una maquina de dificultad "Muy Facil" de la plataforma `HackTheBox`. Meow forma parte de los laboratorios de `Punto de Partida`.

Para completar la maquina ejecute nmap para realizar un escaneo de puertos a la dirrecion ip `10.129.202.44` especificamente el puerto 23/tcp, ya que supe que el puerto esta abierto con el servicio telnet usando el comando `Telnet [DireccionIp]` me conecte al servidor `meow` y proporcionando `root` como nombre de dominio logre ingresar al servidor, usando `ls` listo los contenidos del servidor y encuentro un archivo `flag.txt` con el comando `cat` veo el contenido del archivo y asi encuentro la `flag` resolviendo esta maquina.

___

## Procedimiento

Para atacar la maquina meow se necesita estar en la misma red, conectese a la VPN de `Punto de Partida` usando una de las siguientes opciones:

![Anexo1](/images/Meow/Anexo1.png)

He utilizado el metodo `OVPN` y Kali Linux como sistema principal para este proyecto, Descargue el archivo (.ovpn):

![Anexo2](/images/Meow/Anexo2.png)

Abri una terminal y ejecute el siguiente comando: 

- **sudo openvpn starting_point_R4NC0X.ovpn**

- **El nombre `starting_point_R4NC0X.ovpn` debe ser remplazado por el nombre del archivo que descago en su maquina**

![Anexo3](/images/Meow/Anexo3.png)

Actualice la pagina en el navegador para comprobar la nueva conexion y activamos la maquina haciendo clic en `Maquina de Aparicion`

![Anexo4](/images/Meow/Anexo4.png)

La maquina ya se encuentra activa y ahora muestra la direccion ip 

![Anexo5](/images/Meow/Anexo5.png)

Ahora resuelvo todas las tareas de la maquina, algunas de las tareas son pistas para resolver esta maquina. 

- **Tarea 1 ¿Que significa las siglas VM?**

`Virtual Machine`

- **Tarea 2 ¿Que herramientas utilizamos para interactuar con el sistema operativo para poder emitir comandos a traves de la linea de comandos, como por ejemplo el de iniciar nuestra conexion VPN? Tambien se la conoce como consola o shell**

`Terminal`

- **Tarea 3 ¿Que servicio utilizamos para formar nuestra conexion VPN en los laboratorios HTB?**

`openvpn`

- **Tarea 4 ¿Que herramienta utilizamos para probar nuestra conexion con el objetivo con una solicitud de eco ICPM?**

`Ping`

- **Tarea 5 ¿Como se llama la herramienta mas comun para encontrar puertos abiertos en un objetivo**

`Nmap`

- **Tarea 6 ¿Que servicio identificamos en el puerto 23/tcp durante nuestros escaneos?**

`Telnet`

- **Tarea 7 ¿Que nombre de usuario puede iniciar sesion en el objetivo a traves de telnet con una contraseña en blanco?**

`Root`

- **Enviar Bandera Root**
Para poder encontrar la bandera realice un escaneo a la ip de la maquina usando la herramienta `Nmap`

![Anexo6](/images/Meow/Anexo6.png)

Observe que en el puerto 23 esta abierto el servicio Telnet, entonces escribo el comando `Telnet` con la dirrecion ip.

![Anexo7](/images/Meow/Anexo7.png)

Usando el nombre de usuario predeterminado en el `Meow login` podremos acceder a la maquina `Meow`

![Anexo8](/images/Meow/Anexo8.png)

Usando el comando `ls` vamos a listar todos los elementos que contiene el directorio `root@meow` 

``` bash
root@meow:ls
flag.txt snap
root@meow:cat flag.txt
b40abdfe23665f766f9c61ecba8a4c19
```
La bandera ya fue encontrada, la copio y la pego en `Enviar bandera` 
Una ves enviada la bandera salio un mensaje diciendo `Meow has been Pwned`

___

## Maquina Completada :)



