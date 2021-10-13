
# 构建命令

```
# 7.4版本
docker build --force-rm --build-arg BUILD_VERSION='7.4-fpm-alpine' -t oddoson/basephp:7.4-fpm-alpine  . 

# 7.2版本
docker build --force-rm  -t oddoson/basephp:7.2-fpm-alpine  -f Dockerfile-7.2 . 

# 5.6版本
docker build --force-rm  -t oddoson/basephp:5.6-fpm-alpine   -f Dockerfile-5.6 .


```


# php.ini 配置优化

> 文件位置 /usr/local/etc/php/php.ini


## php错误日志文件
这个是php cli的日志，也就是直接通过 php x.php 执行时的错误日志
/var/log/php_error.log

php-fpm错误日志： /var/log/fpm.error.log

## opcache
更新代码最好手动清理缓存，否则文件多导致不同步的问题！！

1. 默认开启opcache
2. 默认检测文件修改时间 60秒（刷新时间） : opcache.revalidate_freq=60

## max_execution_time
最大执行时间600

## post_max_size
post最大50M

## upload_max_filesize
上传文件最大100M

## memory_limit
内存限制1024M

## disable_functions
禁用不安全函数  

disable_functions = "shell_exec,exec,system,passthru,popen"

---   

# php-fpm 配置优化
主配置文件： /usr/local/etc/php-fpm.conf

自定义配置文件 /usr/local/etc/php-fpm.d/*

新的配置文件直接放在改目录下即可。多个文件按字母顺序一次加载覆盖！！


## request_slowlog_timeout
慢日志5秒，设置为 '0' 表示 'Off'。可用单位：s（秒），m（分），h（小时）或者 d（天）。默认单位：s（秒）。默认值：0（关闭）

request_slowlog_timeout = 3s