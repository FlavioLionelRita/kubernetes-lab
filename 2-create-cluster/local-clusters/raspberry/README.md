


# install docker
```
sudo apt install -y docker.io
```
## run docker without root user
```
sudo usermod -aG docker ${USER}
su - ${USER}
id -nG
```

## verify
```
docker info
```
## create o modify docker daemon.json
```
sudo vim /etc/docker/daemon.json
```
add content
```
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
```
## add limits to cmdline.txt
```
sudo sed -i '$ s/$/ cgroup_enable=cpuset cgroup_enable=memory cgroup_memory=1 swapaccount=1/' /boot/firmware/cmdline.txt
```
verify:
```
sudo cat /boot/firmware/cmdline.txt
```

## Permitir que iptables vea el tráfico en puente
```
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
sudo sysctl --system
```

# Install the Kubernetes packages for Ubuntu

## Add the packages.cloud.google.com atp key
```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```
## Add the Kubernetes repo
```
cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
```
## Update the apt cache and install kubelet, kubeadm, and kubectl
```
sudo apt update && sudo apt install -y kubelet kubeadm kubectl
```
## Disable (mark as held) updates for the Kubernetes packages
```
sudo apt-mark hold kubelet kubeadm kubectl
```

# Initialize the Control Plane
## Generate a bootstrap token to authenticate nodes joining the cluster
```
TOKEN=$(sudo kubeadm token generate)
echo $TOKEN
```
TOKEN: v03flf.zj4f4yk4qm4dpygk

## Initialize the Control Plane
```
sudo kubeadm init --token=${TOKEN} --kubernetes-version=v1.19.4 --pod-network-cidr=10.244.0.0/16
```
result:
```
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 192.168.1.150:6443 --token v03flf.zj4f4yk4qm4dpygk \
    --discovery-token-ca-cert-hash sha256:c645e33843c256f8df008a47485890dada25756418e4a58991d7f22143d62476
```

## copy kubeconfig
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

verify
```
kubectl get nodes
``` 
Error:  0/1 nodes are available: 1 node(s) had taint {node.kubernetes.io/not-ready: }, that the pod didn't tolerate.

## Install a CNI add-on
```
curl -sSL https://raw.githubusercontent.com/coreos/flannel/v0.12.0/Documentation/kube-flannel.yml | kubectl apply -f -
```

# Join the compute nodes to the cluster
Ejecutar en el node slave 1
```
sudo kubeadm join 192.168.1.150:6443 --token v03flf.zj4f4yk4qm4dpygk \
    --node-name slave1 --discovery-token-ca-cert-hash sha256:c645e33843c256f8df008a47485890dada25756418e4a58991d7f22143d62476
```
Ejecutar en el node slave 2
```
sudo kubeadm join 192.168.1.150:6443 --token v03flf.zj4f4yk4qm4dpygk \
    --node-name slave2 --discovery-token-ca-cert-hash sha256:c645e33843c256f8df008a47485890dada25756418e4a58991d7f22143d62476
```

# Validate the cluster
```
kubectl create namespace kube-verify
kubectl apply -f cluster-verify.yaml
```
verify
```
kubectl get all -n kube-verify
```

test http://192.168.1.152:30007/


# referentes
- [install ubuntu on raspberry](https://ubuntu.com/download/raspberry-pi)
- [install kuberntes on raspberry-pi](https://opensource.com/article/20/6/kubernetes-raspberry-pi)
- [install kuberntes on raspberry-pi spanish] (https://translate.google.com/translate?sl=en&tl=es&u=https://opensource.com/article/20/6/kubernetes-raspberry-pi)
- [node port info](https://cloud.ibm.com/docs/containers?topic=containers-nodeport)


https://ubuntu.com/tutorials/how-to-kubernetes-cluster-on-raspberry-pi#5-master-node-and-leaf-nodes

https://blog.bricogeek.com/noticias/raspberry-pi/como-hacer-un-cluster-kubernetes-con-raspberry-pi/

https://www.youtube.com/watch?v=ra6kNSIB1uA



