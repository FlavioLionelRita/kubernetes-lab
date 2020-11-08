
# Test

## add host 

Edit file hosts:
```
sudo vim /etc/hosts
```

Obtener Cluster-Ip 
```
kubectl get svc nginx-ingress --namespace=nginx-ingress
```

Add host
```
10.152.183.13  flaviolrita.local echo1.flaviolrita.local echo2.flaviolrita.local
``` 

## create test
 ```
 kubectl apply -f 01-ns.yaml 
 kubectl apply -f 02-echo1.yaml
 kubectl apply -f 03-echo2.yaml

 ```

## test
```
 curl echo1.flaviolrita.local
 curl echo2.flaviolrita.local
```




