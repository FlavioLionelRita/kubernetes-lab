# Install


install conntrack
```
sudo apt-get update -y
sudo apt-get install -y conntrack
```

install minikube
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 
chmod +x minikube
sudo mv minikube /usr/local/bin/minikube
```

test
```
minikube version
```

## reference 
- [install minikube](https://kubernetes.io/es/docs/tasks/tools/install-minikube/) 

# install kubectl 

averiguar cual es la ultima version
```
curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt
```

instalar la ultima version
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.19.3/bin/linux/amd64/kubectl
chmod +x ./kubectl
mv ./kubectl /usr/local/bin/kubectl
```

test
```
kubectl version
```

## reference 
- [install kubectl](https://kubernetes.io/es/docs/tasks/tools/install-kubectl/) 


# start minikube 
```
sudo minikube start
//sudo minikube start --vm-driver=none
sudo minikube stop
```
# minikue dachboard
```
minikube dashboard
```
# Minikube addons
Listar
```
minikube addons list
```
Enable: helm-tiller, ingress,	ingress-dns, registry, 	registry-creds
```
minikube addons enable helm-tiller
minikube addons enable ingress
minikube addons enable ingress-dns
minikube addons enable registry
minikube addons enable registry-aliases
minikube addons enable registry-creds 
```

# Unistall minikube

```
minikube stop; minikube delete
docker stop (docker ps -aq)
rm -r ~/.kube ~/.minikube
sudo rm /usr/local/bin/localkube /usr/local/bin/minikube
systemctl stop '*kubelet*.mount'
sudo rm -rf /etc/kubernetes/
docker system prune -af --volumes
```


## info

- [kube-dns](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.2.0/manage_network/service_discovery.html)