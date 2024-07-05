+++
date = 2024-07-04
title = "HTB Redeemer WriteUp"
slug = ""
author = ["R4NC0X"]
description = "HackThebox 'Redeemer' WriteUp"
draft = false
tags = [
    "HTB",
    "machine",
    "Linux",
    "Redis",
    "Vulnerability Assessment",
    "Databases",
    "Reconnaissance",
    "Anonymous/guest access",
]
+++

# Redeemer -- HacktheBox

- System: _Linux_
- Difficulty: _Very Easy_
- Plataform: _HacktheBox_

!['Redeemer' Avatar](/images/Redeemer/Redeemer.webp)

___

## Summary

"Redeemer" is a "Very Easy" difficulty machine from the `HackTheBox` platform. Redeemer is part of the `Starting Point` laboratories.

To complete this machine, use nmap to perform port scanning at the ip address `---`. The machine proposes the use of the `Redis` service whose protocol is `6379`, having already confirmed that the port is open, proceed to use the command `redis-cli -h [IpAddress]`, with this I entered the machine and using the `INFO` command I was able to analyze which version of Redis is running as well as know how many clients and keys there are, having all this information with the use of the command `KEYS *` ready the keys that the machine has, one of the 4 is named `flag` so with the `GET flag` command I ready the content by finding the flag and resolving the machine.

___

## Procedure

___

## Completed Machine :)




