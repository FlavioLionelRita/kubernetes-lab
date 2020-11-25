
# Docker commands
remueva las images que no se usan
``` 
docker system prune --all
```
login
```
docker login -u flaviolionelrita -p PASSWORD index.docker.io/flaviolionelrita ;
```
build
```
docker build -t index.docker.io/flaviolionelrita/app-beesion:test . ;
```
push
``` 
docker push index.docker.io/flaviolionelrita/app-beesion:test
```
exec
```
docker exec -it TestControls-WebApp ba
```
stop
```
docker stop TestControls-WebApp
```
Remover
```
docker rm TestControls-WebApp
```

subir una imagen desde un .tar
```
docker load < api-gateway-2-docker-image.tar
```
buscar la imagen por los primeros numeros de image ID
```
docker images | grep 527863
```
hay que taguear la imagen
```
docker tag 5278638e7fc15e977114ca1e9fa4a0e695f1c7acaa5875edc5a1cf3fb864704d api-gateway2
```


docker    

docker build -t app-testris:2.1 . ;


docker run -ti --rm -p 8080:8080 --env-file .env app-testris:2.1


docker run --publish 8000:8080 --detach --name bb bulletinboard:1.0
