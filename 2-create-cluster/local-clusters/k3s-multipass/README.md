## Install
```
snap install multipass
```

## Create the Virtual Machines
```
multipass launch --name k3s-master --cpus 1 --mem 2048M --disk 16G
multipass launch --name k3s-worker1 --cpus 1 --mem 2048M --disk 16G
multipass launch --name k3s-worker2 --cpus 1 --mem 2048M --disk 16G
```

## Create the k3s cluster
```
multipass exec k3s-master -- /bin/bash -c "curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" sh -"
K3S_NODEIP_MASTER="https://$(multipass info k3s-master | grep "IPv4" | awk -F' ' '{print $2}'):6443"
K3S_TOKEN="$(multipass exec k3s-master -- /bin/bash -c "sudo cat /var/lib/rancher/k3s/server/node-token")"
multipass exec k3s-worker1 -- /bin/bash -c "curl -sfL https://get.k3s.io | K3S_TOKEN=${K3S_TOKEN} K3S_URL=${K3S_NODEIP_MASTER} sh -"
multipass exec k3s-worker2 -- /bin/bash -c "curl -sfL https://get.k3s.io | K3S_TOKEN=${K3S_TOKEN} K3S_URL=${K3S_NODEIP_MASTER} sh -"
```

### Verify 
```
multipass list
multipass info k3s-master
multipass exec k3s-master kubectl get nodes
```

## Configure kubectl
```
curl -sfL https://get.k3s.io | sh -s - --write-kubeconfig-mode 644
mkdir ${HOME}/.kube
sudo chmod -R 664 ${HOME}/.kube
multipass exec k3s-master sudo cat /etc/rancher/k3s/k3s.yaml > ${HOME}/.kube/k3s.yaml
sed -ie s,https://127.0.0.1:6443,${K3S_NODEIP_MASTER},g ${HOME}/.kube/k3s.yaml
cat ${HOME}/.kube/k3s.yaml > ${HOME}/.kube/config
```

### Verify
```
kubectl get nodes
```

## Configure cluster node roles and taint
```
kubectl label node k3s-worker1 node-role.kubernetes.io/node=''
kubectl label node k3s-worker2 node-role.kubernetes.io/node=''
kubectl taint node k3s-master node-role.kubernetes.io/master=effect:NoSchedule 
```
### Verify
```
kubectl  get pods -o wide
```

##  Helm installation
```
kubectl -n kube-system create serviceaccount tiller
kubectl create clusterrolebinding tiller --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
helm init --service-account tiller
``` 

## add nginx
```
kubectl create namespace nginx
kubectl run nginx --image=nginx --replicas=3 --expose --port 80 -n nginx
```

# PROBLEM
- problem: It did not work for me to reach the services through nginx
- casuse: nginx conflict with trafik
    - [info](https://dev.to/sr229/how-to-use-nginx-ingress-controller-in-k3s-2ck2)
    I gave up and I will try to install multipass with microk8s  
- solution: I still haven't found it      

<!-- 
## Uninstall cluster
```
multipass stop k3s-master k3s-worker1 k3s-worker2
multipass delete k3s-master k3s-worker1 k3s-worker2
multipass purge
``` 
-->

## references
-[create cluster multipass-k3s](https://levelup.gitconnected.com/kubernetes-cluster-with-k3s-and-multipass-7532361affa3)
-[install multipass](https://multipass.run/docs/installing-on-linux) 



