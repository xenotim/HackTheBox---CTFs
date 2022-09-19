````
for PORT in {0..1000}; do timeout 1 bash -c "</dev/tcp/192.168.0.119/$PORT &>/dev/null" 2>/dev/null && echo "port $PORT is open"; done

```
for port in $(seq 1 1000); do (echo "blah" > /dev/tcp/172.19.0.1/$port && echo "open - $port") 2>/dev/null; done
```

`````













xxxxxxxxxxxxxxxxxxxxxxxxxxxxx