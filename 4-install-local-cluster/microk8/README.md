# Install

## install micrlk8s
```
sudo snap install microk8s --classic
```

## permisios for user 
```
sudo usermod -a -G microk8s flavio
sudo chown -f -R flavio ~/.kube
```
debe reiniciar la maquina.

## addons
```
microk8s enable dns dashboard storage
```




## reference

['Cómo instalar MicroK8s'](https://ubunlog.com/microk8s-una-herramienta-para-desplegar-kubernetes-en-segundos/)
[install microk8s](https://ubuntu.com/tutorials/install-a-local-kubernetes-with-microk8s#2-deploying-microk8s)