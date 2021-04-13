
# Test

## add host 

Edit file hosts:
```
sudo vim /etc/hosts
```

### Obtener IP

Si el cluster es local
```
kubectl get svc nginx-ingress --namespace=nginx-ingress
```
Si el cluster fue creado con multipass
```
multipass info k3s-master
```

Add host
```
10.131.90.115  www.example.com echo1.example.com echo2.example.com
10.131.90.115  www.example.com echo1.example.com echo2.example.com
``` 

## create test
 ```
 kubectl apply -f 01-ns.yaml 
 kubectl apply -f 02-echo1.yaml
 kubectl apply -f 03-echo2.yaml

 ```

## test
```
 curl echo1.example.com
 curl echo2.example.com
```

 ## uninstall
 ```
 kubectl delete -f 03-echo2.yaml
 kubectl delete -f 02-echo1.yaml
 kubectl delete -f 01-ns.yaml 
 ```




