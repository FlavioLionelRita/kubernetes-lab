

# MongoDb en aws


# Crear una instancia en AWS (utilizar la instancia)
micro-blazed-test

# entrar con SSh 
ssh -i "blazedcloud-keypair.pem" ec2-user@18.222.94.191

# agregar el paquete de mongo a la maquina virtual de EC2
echo -e "[mongodb-org-3.6] \nname=MongoDB Repository\nbaseurl=https://repo.mongodb.org/yum/amazon/2013.03/mongodb-org/3.6/x86_64/\ngpgcheck=1 \nenabled=1 \ngpgkey=https://www.mongodb.org/static/pgp/server-3.6.asc" | sudo tee /etc/yum.repos.d/mongodb-org-3.6.repo

# instalar cliente de mongo
sudo yum install -y mongodb-org-shell

# Configurar el cliente de aws
    [ec2-user@ip-10-0-1-77 ~]$ aws configure 
    AWS Access Key ID [None]: AKIA4B6VIBVEWB2MD262
    AWS Secret Access Key [None]: 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
    Default region name [None]: us-east-2
    Default output format [None]: json
    [ec2-user@ip-10-0-1-77 ~]$ 

# download secret
wget https://s3.amazonaws.com/rds-downloads/rds-combined-ca-bundle.pem

# conectarse a mongodb
mongo --ssl --host blazedcloud-docdb.cluster-cetoi8xavrlb.us-east-2.docdb.amazonaws.com:27017 --sslCAFile rds-combined-ca-bundle.pem --username adminblazed --password I5AckBeesion

# conexion desde app
mongodb://adminblazed:I5AckBeesion@blazedcloud-docdb.cluster-cetoi8xavrlb.us-east-2.docdb.amazonaws.com:27017/?ssl=true&ssl_ca_certs=rds-combined-ca-bundle.pem&replicaSet=rs0&readPreference=secondaryPreferred&retryWrites=false