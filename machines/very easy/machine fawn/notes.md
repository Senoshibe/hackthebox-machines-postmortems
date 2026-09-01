# machine fawn terminal history

─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-dbayblsswg]─[~]
└──╼ [★]$ sudo nmap -sV 10.129.1.14
Starting Nmap 7.95 ( https://nmap.org ) at 2026-09-01 09:29 EDT
Nmap scan report for 10.129.1.14
Host is up (0.28s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
Service Info: OS: Unix

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 4.23 seconds
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-dbayblsswg]─[~]
└──╼ [★]$ ftp 10.129.1.14
Connected to 10.129.1.14.
220 (vsFTPd 3.0.3)
Name (10.129.1.14:root): anonymous
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||42545|)
150 Here comes the directory listing.
-rw-r--r--    1 0        0              32 Jun 04  2021 flag.txt
226 Directory send OK.
ftp> cat flag.txt
?Invalid command.
ftp> open flag.txt
Already connected to 10.129.1.14, use close first.
ftp> get flag.txt
local: flag.txt remote: flag.txt
229 Entering Extended Passive Mode (|||63526|)
150 Opening BINARY mode data connection for flag.txt (32 bytes).
100% |*******************************|    32       71.34 KiB/s    00:00 ETA
226 Transfer complete.
32 bytes received in 00:00 (0.11 KiB/s)
ftp> bye
221 Goodbye.
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-dbayblsswg]─[~]
└──╼ [★]$ ls
cacert.der  Documents  flag.txt  my_data   Templates
Desktop     Downloads  Music     Pictures  Videos
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-dbayblsswg]─[~]
└──╼ [★]$ cat flag.txt 
035db21c881520061c53e0536e44f815┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-dbayblsswg]─[~]
└──╼ [★]$ 

---

I've been too used to ssh-ing into virtual machines, so I ran the cat command to try and print the contents of the flag.txt text file. 

Command obviously failed.

Went back to the HackTheBox documentation and found that you're needing to use the GET command. Almost feels like an API call? Anyways, I just accepted it and ran 
```
get flag.txt
```

Nothing seemed to happen. I remember in documentation saying you can run command...
```
bye
```
to get out of FTP connection (?)

Got out back into box. Ran ls to see if the get command retrieved the text file into current directory. 

lo an behold, the file was there so finally ran 
```
cat flag.txt
```
Got the flag, machine rooted.