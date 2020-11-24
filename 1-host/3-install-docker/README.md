# Install


## install docker
```
sudo apt update
sudo apt install apt-transport-https ca-certificates software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
sudo apt update
apt-cache policy docker-ce
sudo apt install docker-ce
sudo systemctl status docker
```

## run docker without root user
```
sudo usermod -aG docker ${USER}
su - ${USER}
id -nG
```

# referece
- [docker](https://www.digitalocean.com/community/tutorials/como-instalar-y-usar-docker-en-ubuntu-18-04-1-es)

- [lightweight images](https://semaphoreci.com/blog/2016/12/13/lightweight-docker-images-in-5-steps.html)
- [lightweight images](https://medium.com/trendyol-tech/how-we-reduce-node-docker-image-size-in-3-steps-ff2762b51d5a)
