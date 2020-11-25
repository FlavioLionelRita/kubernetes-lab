
# minikube 
sudo minikube start -p --vm-driver=none
sudo minikube stop


# minikue dachboard
sudo minikube dashboard

# Minikube addons
    //Listar
    minikube addons list

    //Enable: helm-tiller, ingress,	ingress-dns, registry, 	registry-creds
    minikube addons enable helm-tiller
    minikube addons enable ingress
    minikube addons enable ingress-dns
    minikube addons enable registry
    minikube addons enable registry-aliases
    minikube addons enable registry-creds 