# Install

## install micrlk8s
```
sudo snap install microk8s --classic
```

## permisios for user 
```
sudo usermod -a -G microk8s flavio
sudo chown -f -R flavio ~/.kube
su - ${USER}
```

## addons
```
microk8s enable dns dashboard storage 
microk8s enable host-access

//microk8s disable helm3 prometheus rbac

```

## test
```
microk8s status
```

## create kubeconfig
```
cd $HOME
cd .kube
microk8s config > config
```


## create aliases mk for "microk8s kubectl"
- [how to create aliases](https://linuxize.com/post/how-to-create-bash-aliases/)

## reference
- ['Cómo instalar MicroK8s'](https://ubunlog.com/microk8s-una-herramienta-para-desplegar-kubernetes-en-segundos/)
- ['install microk8s'](https://microk8s.io/docs)
- [install microk8s](https://ubuntu.com/tutorials/install-a-local-kubernetes-with-microk8s#2-deploying-microk8s)
- [create kubeconfig](https://microk8s.io/docs/working-with-kubectl)
- [host-access](https://microk8s.io/docs/addon-host-access)
