# Install

## prerequisites
install conntrack
```
sudo apt-get update -y
sudo apt-get install -y conntrack
```

## install minikube
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 
chmod +x minikube
sudo mv minikube /usr/local/bin/minikube
```

test
```
minikube version
```

### reference 
- [install minikube](https://kubernetes.io/es/docs/tasks/tools/install-minikube/) 


## start minikube 
```
//minikube start
sudo minikube start --vm-driver=none
//sudo minikube stop
```

## Minikube addons
Listar
```
minikube addons list
```
Enable: addons
```
minikube addons enable helm-tiller
minikube addons enable ingress
minikube addons enable ingress-dns
minikube addons enable registry
minikube addons enable registry-aliases
minikube addons enable registry-creds 
minikube addons enable metrics-server
```

## minikue dachboard
```
minikube dashboard
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