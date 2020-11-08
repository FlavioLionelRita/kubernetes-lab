

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

kubectl apply -f service/loadbalancer.yaml

```

# reference
[install nginx 1.9.0](https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-manifests/)
[nginx 1.9.0](https://www.nginx.com/blog/announcing-nginx-ingress-controller-release-1-9-0/)








# nginx realeses
[realeses](https://docs.nginx.com/nginx-ingress-controller/releases/)



# realizar paso 2: Configurar el controlador de Ingress de Nginx en Kubernetes 
- https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-with-cert-manager-on-digitalocean-kubernetes-es