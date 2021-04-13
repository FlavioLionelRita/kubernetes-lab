

# Install 
```
kubectl create ns mariadb 
helm install mariadb bitnami/mariadb -f ./bitnami-helm/values.yaml -n mariadb
```

# Info
## Tip:
```
  Watch the deployment status using the command: kubectl get pods -w --namespace mariadb -l release=mariadb
```
## Services:
```
  echo Primary: mariadb.mariadb.svc.cluster.local:3306
```
## Administrator credentials:
```
  Username: root
  Password : $(kubectl get secret --namespace mariadb mariadb -o jsonpath="{.data.mariadb-root-password}" | base64 --decode)
```

## To connect to your database:

Run a pod that you can use as a client:
``` 
    kubectl run mariadb-client --rm --tty -i --restart='Never' --image  docker.io/bitnami/mariadb:10.5.8-debian-10-r0 --namespace mariadb --command -- bash
``` 
To connect to primary service (read/write):
```
    mysql -h mariadb.mariadb.svc.cluster.local -uroot -p my_database
```

## To upgrade this helm chart:
Obtain the password as described on the 'Administrator credentials' section and set the 'auth.rootPassword' parameter as shown below:
```
      ROOT_PASSWORD=$(kubectl get secret --namespace mariadb mariadb -o jsonpath="{.data.mariadb-root-password}" | base64 --decode)
      helm upgrade mariadb bitnami/mariadb --set auth.rootPassword=$ROOT_PASSWORD
```


# Uninstall 
```
helm uninstall mariadb -n mariadb
kubectl delete ns mariadb 
```

# references
- [bitnamu mysql](https://bitnami.com/stack/mariadb/helm)