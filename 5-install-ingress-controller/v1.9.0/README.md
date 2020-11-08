
# Install
```
kubectl apply -f common/ns-and-sa.yaml
kubectl apply -f rbac/rbac.yaml
kubectl apply -f rbac/ap-rbac.yaml
kubectl apply -f common/default-server-secret.yaml
kubectl apply -f common/nginx-config.yaml
kubectl apply -f common/ingress-class.yaml
kubectl apply -f common/vs-definition.yaml
kubectl apply -f common/vsr-definition.yaml
kubectl apply -f common/ts-definition.yaml
kubectl apply -f common/policy-definition.yaml
kubectl apply -f common/gc-definition.yaml
kubectl apply -f common/global-configuration.yaml
kubectl apply -f deployment/nginx-ingress.yaml
kubectl apply -f daemon-set/nginx-ingress.yaml
kubectl apply -f service/nodeport.yaml
```

# Uninstall
```
kubectl delete -f service/nodeport.yaml
kubectl delete -f daemon-set/nginx-ingress.yaml
kubectl delete -f deployment/nginx-ingress.yaml
kubectl delete -f common/global-configuration.yaml
kubectl delete -f common/gc-definition.yaml
kubectl delete -f common/policy-definition.yaml
kubectl delete -f common/ts-definition.yaml
kubectl delete -f common/vsr-definition.yaml
kubectl delete -f common/vs-definition.yaml
kubectl delete -f common/ingress-class.yaml
kubectl delete -f common/nginx-config.yaml
kubectl delete -f common/default-server-secret.yaml
kubectl delete -f rbac/ap-rbac.yaml
kubectl delete -f rbac/rbac.yaml
kubectl delete -f common/ns-and-sa.yaml
```


# References
[install nginx 1.9.0](https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-manifests/)
[nginx 1.9.0](https://www.nginx.com/blog/announcing-nginx-ingress-controller-release-1-9-0/)
[realeses](https://docs.nginx.com/nginx-ingress-controller/releases/)