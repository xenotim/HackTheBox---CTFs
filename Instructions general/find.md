
find suid files
````
find / -type f -perm -4000 -exec ls -ldb {} \; 2>/dev/null

`````

find files owned by user and discard /proc /var /sys /home

````
find / -type f -user svc_acc 2>/dev/null | grep -v '\/proc/\|\/sys/\|\/var/\|\/home/'

`````
![](https://github.com/xenotim/CTF/blob/main/Instructions%20general/screenshots/find%20user%20owned%20files.png)
![](https://github.com/xenotim/CTF/blob/main/Instructions%20general/screenshots/curl%20-%20POST%20with%20data%2C%20cookie%20and%20header.png)

XXXXXXXXXXXX