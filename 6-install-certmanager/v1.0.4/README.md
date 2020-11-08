
# Install

## install cert-manager
```
kubectl apply --validate=false -f cert-manager.yaml
```

## verifying
```
kubectl get pods --namespace cert-manager
```

## configuration
```
kubectl apply -f letsencrypt-staging.yaml
kubectl apply -f letencrypt-prod.yaml
kubectl apply -f letencrypt-wildcard-certificate.yaml
```

## uninstall
```
kubectl delete -f letsencrypt-staging.yaml
kubectl delete -f letencrypt-prod.yaml
kubectl delete -f letencrypt-wildcard-certificate.yaml
kubectl delete -f cert-manager.yaml
```


kubectl delete -f letencrypt-prod.yaml

# References

[install](https://cert-manager.io/docs/installation/kubernetes/)