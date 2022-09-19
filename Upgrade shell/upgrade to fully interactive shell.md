````
python3 -c 'import pty;pty.spawn("/bin/bash")'

````

````
^Z to background shell

`````

in fullscreen window :
````
stty raw -echo

fg

enter,enter

export TERM=xterm

stty rows 36 cols 190
`````
in seperate fullscreen window:

prints rows and cols
````
stty -a

`````









![](test.png)


xxxxxxxxxxxx