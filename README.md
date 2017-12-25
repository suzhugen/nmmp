# nmmp
nginx,mysql,mongo,php


# build
docker-composer up


# install docker  
base centos.
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2  
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo  
sudo yum install docker-ce  
sudo systemctl enable docker  
sudo systemctl start docker    



# install docker-compose  
curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose  
sudo chmod +x /usr/local/bin/docker-compose   
docker-compose --version  


