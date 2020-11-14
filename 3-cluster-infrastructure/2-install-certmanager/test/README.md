
# Test

TODO: Aun no funciona, hay que ver por que.
# info
https://cert-manager.io/docs/tutorials/acme/ingress/
https://cert-manager.io/docs/usage/ingress/
https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-with-cert-manager-on-digitalocean-kubernetes-es


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




