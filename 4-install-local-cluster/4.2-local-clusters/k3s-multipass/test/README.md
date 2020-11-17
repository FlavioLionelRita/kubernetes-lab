# Info
IMPORTANT: It did not work for me to access the services by nginx apparently due to conflict with TRAFIK

#  test
```
kubectl create namespace test
helm install mysql bitnami/mysql -n test
kubectl get pod -n test
kubectl create deploy nginx2 --image=nginx -n test
kubectl create svc nodeport nginx2 --tcp=30001:80 --node-port=30001 -n test
K3S_NODE_HOST_MASTER=(http://$(multipass info k3s-master | grep "IPv4" | awk -F' ' '{print $2}'))
curl -XGET -s -I -o /dev/null -w "%{http_code}\n" $K3S_NODE_HOST_MASTER:30001
curl $K3S_NODE_HOST_MASTER:30001
kubectl apply -f ingress-controller.yaml
curl nginx2.10.43.164.137.xip.io
```

# Clear tests
```
kubectl delete -f ingress-controller.yaml
helm uninstall mysql
kubectl delete svc nginx2  -n test
kubectl delete deploy nginx2 -n test
kubectl delete svc nginx -n nginx
kubectl delete pod nginx -n nginx

```

## TODO: 
- volver a instalar nginx y los pasos para ver si se puede acceder a una aplicacion.
- instalar las aplicaciones desde https://bitnami.com/stacks/helm 


## references
-[create cluster multipass-k3s](https://levelup.gitconnected.com/kubernetes-cluster-with-k3s-and-multipass-7532361affa3)
-[install multipass](https://multipass.run/docs/installing-on-linux) 



