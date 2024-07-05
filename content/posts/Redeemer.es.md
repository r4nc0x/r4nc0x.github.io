+++
date = 2024-07-04
title = "HTB Redeemer WriteUp"
slug = ""
author = ["R4NC0X"]
description = "HackThebox 'Redeemer' WriteUp"
draft = false
tags = [
    "HTB",
    "Maquina",
    "Linux",
    "Redis",
    "Evaluacion de vilnerabilidad",
    "Base de datos",
    "Reconocimiento",
    "Acceso anonimo/invitado",
]
+++

# Redeemer -- HacktheBox

- Sistema: _Linux_
- Dificultad: _Muy Facil_
- Plataforma: _HacktheBox_

!['Redeemer' Avatar](/images/Redeemer/Redeemer.webp)

___

## Resumen 

"Redeemer" es una maquina de dificultad "Muy Facil" ded la plataforma `HackTheBox`. Redeemer forma parte de los laboratorios de `Punto de Partida`.

Para completar esta maquina utilize nmap para realizar escaneo de puertos a la dirrecion ip `---`, La maquina propone el uso del servicio `Redis` cuyo protocolo es el `6379` ya confirmado que el puerto esta abierto procedi a usar el comando `redis-cli -h [DireccionIp]`, con esto ingrese a la maquina y usando el comando `INFO` pude analizar que version de redis esta funcionando asi como saber cuantos clientes y keys hay, teniendo toda esta informacion con el uso del comando `KEYS *` listo las keys que tiene la maquina, una de las 4 lleva el nombre de `flag` por lo que con el comando `GET flag` listo el contenido encontrando la bandera y resolviendo la maquina.

___

## Procedimiento

___

## Maquina Completada :)



