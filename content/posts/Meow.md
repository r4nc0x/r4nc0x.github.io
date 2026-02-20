+++
date = 2024-06-27
title = "HTB Meow WriteUp"
slug = ""
author = ["R4NC0X"]
description = "HackThebox 'Meow' WriteUp"
draft = false
tags = [
    "HTB",
    "machine",
    "Linux",
    "Telnet",
    "Protocols",
    "Reconnaissance",
    "Weak Credentials",
    "Misconfiguration",
]
+++

# Meow -- HacktheBox

- System: _Linux_
- Difficulty: _Very Easy_
- Plataform: _HacktheBox_

!['Meow' Avatar](/images/Meow/Meow.webp)

___

## Summary

"Meow" is a "Very Easy" difficulty machine from the `HackTheBox` platform. Meow is part of the `Starting Point` laboratories.

To complete the machine run nmap to perform a port scan to the IP address `10.129.202.44` specifically port 23/tcp, since I knew that the port is open with the telnet service using the command `Telnet [IPAddress]` me connect to the `meow` server and providing `root` as the domain name I manage to enter the server, using `ls` I list the contents of the server and find a file `flag.txt` with the command `cat` I see the contents of the file and This is how I find the `flag` solving this machine.

___

## Procedure

To attack the meow machine you need to be on the same network, connect to the `Starting Point` VPN using one of the following options:

![Anexo1](/images/Meow/Anexo1.png)

I have used `OVPN` method and Kali Linux as main system for this project, Download the file (.ovpn):

![Anexo2](/images/Meow/Anexo2.png)

Open a terminal and run the following command:

- **sudo openvpn starting_point_R4NC0X.ovpn**

- **The name `starting_point_R4NC0X.ovpn` should be replaced with the name of the file you downloaded to your machine**

![Anexo3](/images/Meow/Anexo3.png)

Refresh the page in the browser to check the new connection and activate the machine by clicking on `Spawn Machine`

![Anexo4](/images/Meow/Anexo4.png)

The machine is already active and now shows the IP address

![Anexo5](/images/Meow/Anexo5.png) 

Now I solve all the tasks of the machine, some of the tasks are clues to solve this machine.

- **Task 1 What does the acronym VM mean?**

`Virtual Machine`

- **Task 2 What tools do we use to interact with the operating system to be able to issue commands through the command line, such as starting our VPN connection? It is also known as a console or shell**

`Terminal`

- **Task 3 What service do we use to form our VPN connection in the HTB laboratories?**

`openvpn`

- **Task 4 What tool do we use to test our connection to the target with an ICPM echo request?**

`Ping`

- **Task 5 What is the name of the most common tool to find open ports on a target**

`nmap`

- **Task 6 What service do we identify on port 23/tcp during our scans?**

`Telnet`

- **Task 7 What username can log into the target via telnet with a blank password?**

`Root`

- **Send Root Flag**
In order to find the flag, scan the machine's IP using the `Nmap` tool.

![Anexo6](/images/Meow/Anexo6.png)

Note that the Telnet service is open on port 23, so I write the command `Telnet` with the IP address.

![Anexo7](/images/Meow/Anexo7.png)

Using the default username in the `Meow login` we can access the `Meow` machine

![Anexo8](/images/Meow/Anexo8.png)

Using the `ls` command we will list all the elements contained in the `root@meow` directory

``` bash
root@meow:ls
flag.txt snap
root@meow:cat flag.txt
b40abdfe23665f766f9c61ecba8a4c19
```

The flag was already found, I copied it and pasted it into `Send Flag`.
Once I sent the flag, a message appeared that said `Meow has been Pwned`

___

## Completed Machine :)




