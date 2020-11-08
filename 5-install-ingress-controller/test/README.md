
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
10.152.183.13   example.local echo1.example.local echo2.example.local echo2.example.local
``` 

## create test
 ```
 kubectl apply -f 01-ns.yaml 
 kubectl apply -f 02-echo1.yaml
 kubectl apply -f 03-echo2.yaml

 ```

## test
```
 curl echo1.example.local
 curl echo2.example.local
```




