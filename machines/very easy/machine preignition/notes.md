Funny thing to note here is from the official write up document for the exercise (see references) the link to the common.txt file in the instructions is actually wrong:
(refer to screenshots folder)

Had to right click the hyperlink to the common.txt file and use that URL instead with the sudo wget command. 

Another interesting thing to note is, in manpage for gobuster it says the flag for finding .php pages is -x .php, whereas on google it's -x php

The latter was accepted in one of the questions with the hackthebox exercises...

┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-xkhn2ecnmz]─[~]
└──╼ [★]$ ping ^C^C
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-xkhn2ecnmz]─[~]
└──╼ [★]$ ping 10.129.187.44
PING 10.129.187.44 (10.129.187.44) 56(84) bytes of data.
64 bytes from 10.129.187.44: icmp_seq=1 ttl=63 time=278 ms
64 bytes from 10.129.187.44: icmp_seq=2 ttl=63 time=278 ms
^C
--- 10.129.187.44 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 277.571/277.590/277.610/0.019 ms
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-xkhn2ecnmz]─[~]
└──╼ [★]$ sudo nmap -sV 10.129.187.44
Starting Nmap 7.95 ( https://nmap.org ) at 2026-09-03 09:18 EDT
Nmap scan report for 10.129.187.44
Host is up (0.28s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
80/tcp open  http    nginx 1.14.2

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 13.68 seconds
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-xkhn2ecnmz]─[~]
└──╼ [★]$ sudo apt install golang-go
golang-go is already the newest version (2:1.24~2).
golang-go set to manually installed.
The following package was automatically installed and is no longer required:
  linux-image-6.12.73+deb13-amd64
Use 'sudo apt autoremove' to remove it.

Summary:
  Upgrading: 0, Installing: 0, Removing: 0, Not Upgrading: 533
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-xkhn2ecnmz]─[~]
└──╼ [★]$ sudo apt install gobuster
gobuster is already the newest version (3.6.0-1+b10).
The following package was automatically installed and is no longer required:
  linux-image-6.12.73+deb13-amd64
Use 'sudo apt autoremove' to remove it.

Summary:
  Upgrading: 0, Installing: 0, Removing: 0, Not Upgrading: 533
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-xkhn2ecnmz]─[~]
└──╼ [★]$ wget https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/WebContent/common.txt -O /usr/share/wordlists/common.txt
/usr/share/wordlists/common.txt: Permission denied
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-xkhn2ecnmz]─[~]
└──╼ [★]$ sudo gobuster dir -w /usr/share/wordlists/common.txt -u 10.129.187.44
Error: error on parsing arguments: wordlist file "/usr/share/wordlists/common.txt" does not exist: stat /usr/share/wordlists/common.txt: no such file or directory
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-xkhn2ecnmz]─[~]
└──╼ [★]$ wget https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/WebContent/common.txt -O /usr/share/wordlists/common.txt
/usr/share/wordlists/common.txt: Permission denied
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-xkhn2ecnmz]─[~]
└──╼ [★]$ sudo wget https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/WebContent/common.txt -O /usr/share/wordlists/common.txt
--2026-09-03 09:21:04--  https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/WebContent/common.txt
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.109.133, 185.199.108.133, 185.199.111.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.109.133|:443... connected.
HTTP request sent, awaiting response... 404 Not Found
2026-09-03 09:21:05 ERROR 404: Not Found.

┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-xkhn2ecnmz]─[~]
└──╼ [★]$ sudo wget https://github.com/danielmiessler/SecLists/raw/master/Discovery/Web-Content/common.txt -O /usr/share/wordlists/common.txt
--2026-09-03 09:22:20--  https://github.com/danielmiessler/SecLists/raw/master/Discovery/Web-Content/common.txt
Resolving github.com (github.com)... 4.237.22.38
Connecting to github.com (github.com)|4.237.22.38|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/common.txt [following]
--2026-09-03 09:22:21--  https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/common.txt
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.109.133, 185.199.108.133, 185.199.111.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.109.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 38536 (38K) [text/plain]
Saving to: ‘/usr/share/wordlists/common.txt’

/usr/share/wordlis 100%[================>]  37.63K  --.-KB/s    in 0s      

2026-09-03 09:22:21 (104 MB/s) - ‘/usr/share/wordlists/common.txt’ saved [38536/38536]

┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-xkhn2ecnmz]─[~]
└──╼ [★]$ sudo gobuster dir -w /usr/share/wordlists/common.txt -u 10.129.187.44
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.129.187.44
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/admin.php            (Status: 200) [Size: 999]
Progress: 4752 / 4752 (100.00%)
===============================================================
Finished
===============================================================
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-xkhn2ecnmz]─[~]
└──╼ [★]$ sudo gobuster dir -w /usr/share/wordlists/common.txt -u 10.129.187.44^C
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-xkhn2ecnmz]─[~]
└──╼ [★]$ 
