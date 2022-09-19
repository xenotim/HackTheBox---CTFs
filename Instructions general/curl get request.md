
````

curl -i -H "Accept: application/json" -H "Content-Type: application/json" -X GET http://hostname/resource

`````

````
curl -i http://admin:admin@178.62.91.197:31699/search.php?search=flag

`````

````
curl -X POST -d '{"search":"flag"}' -b 'PHPSESSID=cookievalue' -H 'Content-Type: application/json)' http://ip:port

`````

````
awk -F[:] '{print $2}' json.txt | grep '[/w,]' | grep '[A-Z a-z]' | sed 's/","//' | grep '[/w,]' | grep '[A-Z a-z]' | sed 's/",//' | sed 's/"//'

`````

````
for i in $(<towns.txt); do curl -s 159.65.89.165:32433/api.php/city/$i -X PUT -d '{"city_name":"flag"}' -H 'Content-Type: application/json'; done

`````

````
apropos sudo

`````

List listening interfaces
````
ss -l -4 | grep -v "127\.0\.0" | grep "LISTEN" | wc -l

`````


XXXXXXXXXXXXX


