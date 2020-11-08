
# Test

TODO: Aun no funciona, hay que ver por que.

## create test
 ```
 kubectl apply -f 02-echo1.yaml
 kubectl apply -f 03-echo2.yaml

 ```
## uninstall

kubectl delete -f 02-echo1.yaml
kubectl delete -f 03-echo2.yaml


## test
```
 curl echo1.example.com
 curl echo2.example.com
```




