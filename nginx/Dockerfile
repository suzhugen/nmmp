# docker build -t mynginx .
FROM nginx:1.13.7
MAINTAINER "odd"
LABEL author="odd" \
      description="nginx" 

# -v /data/nginx/conf/nginx.conf:/etc/nginx/nginx.conf
# -v /data/nginx/conf/conf.d/:/etc/nginx/conf.d/
# default www dir : /usr/share/nginx/html

RUN mkdir -p /data/nginx/conf
RUN mkdir -p /data/nginx/logs


# VOLUME [ "/etc/nginx/conf.d/","/var/log/nginx/" ]

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

  
