
# procedere privesc to root
--> /home/augustus is mounted in docker environment with root privileges
--> make a copy to /home/augustus of bash hosted from attacker system with python3 http server
--> make bash suid file: chmod 4777
--> SSH: ./bash -p --> root
Changes in docker environment are immediately refleced in SSH /home/augustus!
Since we are root in docker chmod is possible --> SUID 4777 file!
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/GoodGames/screenshots/suid%20bash%204777.png)

## ssh into augustus
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/GoodGames/screenshots/ssh%20into%20augustus.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/GoodGames/screenshots/suid%20bash%20highlighted.png)

Troubles with bash from SSH login --> moans about a missing library --> host your own bash file from attacker system 
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/GoodGames/screenshots/troubles%20with%20bash%20on%20ssh.png)
Host your own bash file with python3 http server and wget it on host system

## troubles bash solution --> host your system bash file
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/GoodGames/screenshots/troubles%20bash%20solution%20--%20host%20your%20system%20bash.png)

Escalate to root --> Running SUID file with -p flag

## troubles bash error
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/GoodGames/screenshots/troubles%20bash%20error.png)


XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX