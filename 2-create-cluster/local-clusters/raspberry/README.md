


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


https://translate.google.com/translate?sl=en&tl=es&u=https://opensource.com/article/20/6/kubernetes-raspberry-pi

# referentes
- [install ubuntu on raspberry](https://ubuntu.com/download/raspberry-pi)
- [install kuberntes on raspberry-pi](https://opensource.com/article/20/6/kubernetes-raspberry-pi)


https://ubuntu.com/tutorials/how-to-kubernetes-cluster-on-raspberry-pi#5-master-node-and-leaf-nodes

https://blog.bricogeek.com/noticias/raspberry-pi/como-hacer-un-cluster-kubernetes-con-raspberry-pi/

https://www.youtube.com/watch?v=ra6kNSIB1uA



