# nmmp
nginx,mysql,mongo,php

## env require
docker-ce-17.09.1.ce
docker-compose version 1.18.0

# build and run
cd .  
docker-compose up -d  

# build new or latest images
docker-compose build --pull

### compose  
docker-compose restart #重启所有容器
docker-compose restart App1  #重启App1
docker-compose exec App1 bash

# nginx  
 -v /data/nginx/conf/nginx.conf:/etc/nginx/nginx.conf
站点配置： -v /data/nginx/conf/conf.d/:/etc/nginx/conf.d/
默认文件位置： /usr/share/nginx/html

# install docker  
base on centos.  
sudo yum install -y yum-utils \\  
  device-mapper-persistent-data \\  
  lvm2  
sudo yum-config-manager \\  
    --add-repo \\  
    https://download.docker.com/linux/centos/docker-ce.repo  
sudo yum install docker-ce  
sudo systemctl enable docker  
sudo systemctl start docker    



# install docker-compose  
curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose   
docker-compose --version  


