# nmap

## scan ports
````
nmap -p- 10.10.11.143 -oN nmap-all-ports -v --min-rate 1000 -T4

`````

## namp all ports
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/nmap%20all%20ports.png)

## Scan versions and services
````
nmap -sCV 10.10.11.143 -p 22,80,443 -v -oN nmap-services --min-rate 1000 -T4


`````



# gobuster
````
gobuster dir -u http://10.10.11.143 -w /usr/share/wordlists/dirb/common.txt -o gobuster-main


`````

## goubster main domain
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/gobuster%20main.png)

# domain

## just a default apache site
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/Paper%20domain.png)

# burpsuite
## office.paper
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/burpsuite%20response%20new%20domain%20name.png)

## domain: office.paper
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/domain%20office.paper.png)

## Footer reveals wordpress
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/domain%20office.paper%20footer%20reveals%20wordpress.png)

# wpscan
## wpscan snippet
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/wpscan.png)

## wordpress 5.2.3 exploit
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/wordpress%2052.3%20exploit.png)

## http://office.paper/?static=1 --> new domain
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/new%20domain.png)

## login: chat.office.paper
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/rocket.chat%20login.png)

## register on rocket.chat
## http://chat.office.paper/register/8qozr226AhkCHZdyY
## dashboard
## rocket chat
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/rocket%20chat.png)

## chat snippet: bot called: recyclops
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/rocket%20chat%20snippet%20interesting.png)

## recyclops bot
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/recyclops%20bot.png)

## recyclops bot cammand
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/recyclops%20bot%20command.png)


rocket chat path traversal
![](rocket chat path traversal 1.png)

## application called hubot is running
## .env file may containing sensitive data
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/rocketchat%20config%20git.png)

//hubot directory
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/hubot%20directory.png)

## hubot .env file
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/hubot%20.env%20file.png)

## password: Queenofblad3s!23
## user: dwight
##  /etc/passwd
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/etc%20passwd.png)

# ssh
## ssh as dwight with obtained password
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/ssh%20as%20dwight.png)

## user.txt
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Paper/screenshots/user.txt.png)
