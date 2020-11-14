
# Install
```
sudo apt update
sudo apt install mariadb-server
sudo systemctl status mariadb
mysql -V
```
# Securing MariaDB
Importante: 
- En las dos primera opciones ir por N (no ingresar clave para root ni cambiarla, las demas opciones ir pot Y)
- No cambiar nunca la configuracion de root dado que lo usa el sistema para las actualizaciones.
```
sudo mysql_secure_installation
```
## Create account admin

```
sudo mysql
GRANT ALL ON *.* TO 'admin'@'localhost' IDENTIFIED BY 'admin' WITH GRANT OPTION;
FLUSH PRIVILEGES;
exit;
```

# test
```
sudo mysqladmin version
mysqladmin -u admin -p version
mysql -u admin -p
```

# uninstall
```
sudo service mysql stop
sudo apt-get --purge remove "mysql*"
sudo mv /etc/mysql/ /tmp/mysql_configs/
vi /etc/apt/sources.list
sudo apt-get update
```

# refrences
- [install mariadb](https://www.digitalocean.com/community/tutorials/how-to-install-mariadb-on-ubuntu-18-04-es)
- [uninstall mariadb](https://londonappdeveloper.com/2015/03/30/how-to-completely-uninstall-mariadb-from-a-debian-7-server/)