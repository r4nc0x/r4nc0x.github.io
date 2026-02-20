+++
date = 2024-07-02
title = "HTB Fawn WriteUp"
slug = ""
author = ["R4NC0X"]
description = "HackThebox 'Fawn' WriteUp"
draft = false
tags = [
    "HTB",
    "machine",
    "Linux",
    "Ftp",
    "Protocols",
    "Reconnaissance",
    "Anonymous/guest access",
]
+++

# Fawn -- HacktheBox

- System: _Linux_
- Difficulty: _Very Easy_
- Plataform: _HacktheBox_

!['Fawn' Avatar](/images/Fawn/Fawn.webp)

___

## Summary

"Fawn" is a "Very Easy" difficulty machine from the `HackTheBox` platform. Fawn is part of the `Starting Point` laboratories.

To complete this machine run nmap to perform a port scan to the IP address `10.129.219.195`, the Fawn machine deals with the "FTP" protocol so my scan to the machine resulted in an open port 21/TCP since I knew that it is an FTP port, use the command `ftp [IpAddress]` I connect to the machine with a default name `anonymous` and with a blank password I enter the machine, inside the machine I execute the command `ls` To list the contents, the search result gives me a file `flag.txt` and with the `get` command I download the file to my machine, I do a `cat flag.txt` and that's how I get the flag of the machine Fawn

___

## Procedure

We start by solving the machine's Tasks, some of the tasks are clues to solve the machine.

- **Task 1 What does the 3-letter acronym FTP mean?**

`File Transfer Protocol`

- **Task 2 What port does the FTP service usually listen on?**

`21`

- **Task 3 What acronym is used for the version of FTP secured by running the SSH protocol?**

`sftp`

- **Task 4 What is the command we can use to send an ICMP echo request to test our connection with the target?**

`Ping`

- **Task 5 Based on your scans, what version of FTP is running on the destination?**

`vsftpd 3.0.3`

- **Task 6 Based on your analysis, what type of operating system is running on the target?**

`Unix`

- **Task 7 What is the command that we must execute to display the help menu of the 'ftp' client?**

`ftp -h`

- **Task 8 What is the username used on FTP when you want to log in without having an account?**

`Anonymous`

- **Task 9 What is the response code we received for the FTP message 'Login Successful'?**

`230`

- **Task 10 There are a couple of commands that we can use to list the files and directories available on the FTP server. One is to say. What is the other common way to list files on a Linux system?**

`ls`

- **Task 11 What is the command used to download the file that we found on the FTP server?**

`get`

- **Send Root Flag**

In order to find the flag, scan the machine's IP using the `Nmap` tool.

![Anexo1](/images/Fawn/Anexo1.png)

Note that there is a single open port `21/tcp`, it is an `FTP` service, the scan also shows us important data such as version, login, and permissions.

![Anexo2](/images/Fawn/Anexo2.png)

Using the command `ftp [IpAddress]` I enter and it asks me for a username, ftp provides a user by default, so using the name `anonymous` and with an empty password I manage to enter the machine.

![Anexo3](/images/Fawn/Anexo3.png)

Once inside the machine, use `ls` to list contents and notice that there is a file called `flag.txt` with the `get` command I download it to my machine.

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
On my machine with the `cat` command I discover the flag.

``` bash
❯ cat flag.txt
───────┬──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: flag.txt
───────┼──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ 035db21c88152006**************

```
I enter the flag in the last Task of the machine `Send Flag`.

Once the flag was sent, a message came out saying `Fawn has been Pwned`.

![Anexo4](/images/Fawn/Anexo4.png)
___

## Completed Machine :)




