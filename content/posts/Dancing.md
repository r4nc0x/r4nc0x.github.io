+++
date = 2024-07-03
title = "HTB Dancing WriteUp"
slug = ""
author = ["R4NC0X"]
description = "HackThebox 'Dancing' WriteUp"
draft = false
tags = [
    "HTB",
    "machine",
    "Windows",
    "Protocols",
    "Smb",
    "Reconnaissance",
    "Anonymous/guest access",
]
+++

# Dancing -- HacktheBox

- System: _Windows_
- Difficulty: _Very Easy_
- Plataform: _HacktheBox_

!['Dancing' Avatar](/images/Dancing/Dancing.png)

___

## Summary

"Dancing" is a "Very Easy" difficulty machine from the `HackTheBox` platform. Dancing is part of the `Starting Point` laboratories.

To complete the machine, run nmap to perform a port scan to the IP address `10.129.22.109`, the machine proposes the use of a service that is `SMB` [Server Message Block] so I knew that my scan would have to focus on port `445`. Since I knew which service is open using the command `smbclient -L [IpAddress]`, I listed the machine's Actions and proceeded to try to enter each of them with the command `smbclient -N \\\\10.129.22.109\ \[Sharename]`, the only action I could log into without a password was `WorkShares`. Once inside, ready with `dir` the contents and I find that there are two directories `Amy.J` and `James.P`, I entered the `Amy.J` directory using the `cd` command, I proceeded to review its contents and I did not find the flag so I went back to the main directory using `cd ..` and proceeded to enter the `James.P` directory by doing `dir` I found a file `flag.txt`, using the command `more flag.txt` ready the content finding the flag and solving the machine.

___

## Procedure

Start by solving the Machine Tasks, some of the tasks are clues to solve the machine.

- **Task 1 What does the three-letter acronym SMB mean?**

`server message block`

- **Task 2 What port does SMB operate on?**

`445`

- **Task 3 What is the service name for port 445 that appeared in our Nmap scan?**

`microsoft-ds`

- **Task 4 What is the 'flag' or 'switch' that we can use with the smbclient utility to 'list' the actions available in Dancing?**

`-L`

- **Task 5 How many actions are there in Dancing?**

`4`

- **Task 6 What is the name of the share that we can finally access with a blank password?**

`WorkShares`

- **Task 7 What is the command that we can use within the SMB shell to download the files we find?**

`get`

- **Send Root Flag**

To find the flag perform a port scan to the machine's IP address using the `nmap` tool.

![Anexo1](/images/Dancing/Anexo1.png)

How to scan port `445` of the machine only shows me the data of the `microsoft-ds` service.

![Anexo2](/images/Dancing/Anexo2.png)

Using the command `smbclient -L [IpAddress]` list all the machine's Actions to see which of the 4 shown can be accessed without a password.

![Anexo3](/images/Dancing/Anexo3.png)

Since I found the Action that allows me to log in without a password, use the command `smbclient -N \\\\10.129.22.109\\WorkShares`.

![Anexo4](/images/Dancing/Anexo4.png)

Once inside I proceed to list all the contents of the main directory with the `dir` command, finding that there are two directories.

``` bash
smb: \> dir
  .                                   D        0  Mon Mar 29 03:22:01 2021
  ..                                  D        0  Mon Mar 29 03:22:01 2021
  Amy.J                               D        0  Mon Mar 29 04:08:24 2021
  James.P                             D        0  Thu Jun  3 03:38:03 2021

		5114111 blocks of size 4096. 1753536 blocks available
smb: \> 

```
First I enter the `Amy.J` directory with the `cd` command and proceed to list all the contents found in it.

``` bash
smb: \> cd Amy.J
smb: \Amy.J\> dir
  .                                   D        0  Mon Mar 29 04:08:24 2021
  ..                                  D        0  Mon Mar 29 04:08:24 2021
  worknotes.txt                       A       94  Fri Mar 26 06:00:37 2021

		5114111 blocks of size 4096. 1753520 blocks available
smb: \Amy.J\> 

```
I find a file called `worknotes.txt` and with the `more` command I read the contents of the file.

``` bash
- start apache server on the linux machine
- secure the ftp server
- setup winrm on dancing 

```
The `worknotes.txt` file did not contain the flag of this machine so with the `cd ..` command I returned to the main directory and then entered the `James.P` directory and ready the contents of that directory.

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
Notice that there is a file called `flag.txt` so feel free to view its contents to find the flag.

``` bash
5f61c10dffbc77a704d76016a2******

```
I enter the flag in the last Task of the machine `Send Flag`.

Once the flag was sent, a message came out saying `Dancing has been Pwned`.

![Anexo5](/images/Dancing/Anexo5.png)
___

## Completed Machine :)




