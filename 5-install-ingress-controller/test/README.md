
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
10.152.183.55   www.example.com echo1.example.com echo2.example.com
``` 

## create test
 ```
 kubectl apply -f 01-ns.yaml 
 kubectl apply -f 02-echo1.yaml
 kubectl apply -f 03-echo2.yaml

 ```

 ## unstall
 ```
 kubectl delete -f 03-echo2.yaml
 kubectl delete -f 02-echo1.yaml
 kubectl delete -f 01-ns.yaml 
 ```

## test
```
 curl echo1.example.com
 curl echo2.example.com
```




