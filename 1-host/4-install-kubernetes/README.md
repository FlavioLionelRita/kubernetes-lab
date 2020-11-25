# Install

## Averiguar cual es la ultima version
```
curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt
```

## instalar la ultima version
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.19.3/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```


## permisios for user 
```
sudo chown -f -R flavio ~/.kube
su - ${USER}
```

## test
```
kubectl version
```

# reference 
- [install kubectl](https://kubernetes.io/es/docs/tasks/tools/install-kubectl/) 

