
# Listar  (filtrado por puerto, ejemplo: 9456)
    netstat -putona | grep 9456
    ps x | grep 9456
# ver espacio en disco
    df -h  
# agregar host (hay que hacerlo con sudo su)
   echo "192.168.102.135 verdaccio.blazedpath.local" >> /etc/hosts
# ver variable de entorno
  printenv 

# liberar espacio en Virtual Box
Liberar espacio en VM

## En maquina virtual
	sudo dd if=/dev/zero of=zerofillfile bs=1M
	sudo rm zerofillfile
## En el Host
```
cd C:/Program Files/Oracle/VirtualBox
VBoxManage.exe modifymedium "C:\Users\Beesion\VirtualBox VMs\Kubernetes\blzCloud\xubuntu 18.04 Buider-disk1.vdi" -compact
```

# aumentar el tamano de VM
apagar la maquina virtual y sobre el host
```
cd C:/Program Files/Oracle/VirtualBox
VBoxManage.exe modifyhd "C:\Users\Beesion\VirtualBox VMs\Kubernetes\blzCloud\xubuntu 18.04 Buider-disk1.vdi" --resize 65536
```

## references:
-[increase zise disk](http://duenaslerin.com/aumentar-tamano-disco-virtual-virtualbox/)