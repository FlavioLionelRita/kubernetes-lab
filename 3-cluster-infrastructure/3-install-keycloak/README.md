

# Create DB
```
DROP DATABASE keycloak;
CREATE DATABASE keycloak;
CREATE USER 'keycloak'@'%' IDENTIFIED BY 'keycloak';
GRANT ALL PRIVILEGES ON keycloak.* TO 'keycloak'@'%';
FLUSH PRIVILEGES;
```

## test
```
mysql -u keycloak -p
```

apk update
    apk add mysql-client
mysql --host=10.0.1.1 --user=keycloak --password=keycloak keycloak

# add host
10.152.183.55   keycloak.example.com


# Install 

## From kubernetes yaml
```
kubectl create ns keycloak 
kubectl apply -f ./k8s/keycloak.yaml
```
### Uninstall 
```
kubectl delete -f ./k8s/keycloak.yaml 
```

## From Bitnami Helm
```
kubectl create ns keycloak 
helm install keycloak bitnami/keycloak -f ./bitnami/values.yaml -n keycloak
```

### NOTES:
** Please be patient while the chart is being deployed **
#### Keycloak can be accessed through the following DNS name from within your cluster:

    keycloak.keycloak.svc.cluster.local (port 80)

#### To access Keycloak from outside the cluster execute the following commands:
##### Get the Keycloak URL by running these commands:

  NOTE: It may take a few minutes for the LoadBalancer IP to be available.
        You can watch its status by running 'kubectl get --namespace keycloak svc -w keycloak'
```
    export SERVICE_PORT=$(kubectl get --namespace keycloak -o jsonpath="{.spec.ports[0].port}" services keycloak)
    export SERVICE_IP=$(kubectl get svc --namespace keycloak keycloak -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
    echo "http://${SERVICE_IP}:${SERVICE_PORT}/auth"
```

##### Access Keycloak using the obtained URL.
##### Access the Administration Console using the following credentials:
```
  echo Username: user
  echo Password: $(kubectl get secret --namespace keycloak keycloak-env-vars -o jsonpath="{.data.KEYCLOAK_ADMIN_PASSWORD}" | base64 --decode)
```

### Uninstall 
```
helm uninstall keycloak -n keycloak
kubectl delete ns keycloak 
```




## references
[keycloak on kubernetes](https://www.keycloak.org/getting-started/getting-started-kube)
[keycloak bitnami](https://bitnami.com/stack/keycloak/helm)
[OpenID](http://www.arquitectoit.com/api-management/breve-introduccion-open-id-connect/)
[OAuth2 OpenID](https://www.returngis.net/2019/04/oauth-2-0-openid-connect-y-json-web-tokens-jwt-que-es-que/)
