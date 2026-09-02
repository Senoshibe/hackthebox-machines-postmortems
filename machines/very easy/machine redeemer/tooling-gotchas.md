nmap -sV [IP ADDRESS] scans the top 1000 ports according to man nmap

Whereas nmap -p- -sV [IP ADDRESS] scans all ports, hence why the former wasn't able to find the redis server, whereas the latter did.