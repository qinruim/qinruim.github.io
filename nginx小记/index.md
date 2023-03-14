# nginx小坑

# nginx小坑

## 1.nginx

### 安装nginx：

```shell
sudo apt install nginx
```

查看nginx状态：

```shell
systemctl status nginx
```

需要配置防火墙，否则无法访问80和443端口，使用ufw评为配置

### 安装ufw:

```shell
sudo apt install ufw
```

查看ufw状态：

```shell
sudo ufw status
```

启用 ‘Nginx Full’ profile，它包含了80和443这两个端口：

```shell
sudo ufw allow 'Nginx Full'
```

通过以下命令来启动UFW服务并使其在启动时启动（一般在完成默认配置后再重启）：

```shell
sudo ufw enable
```

### nginx默认位置：

- 所有的 Nginx 配置文件都在`/etc/nginx/`目录下。
- 主要的 Nginx 配置文件是`/etc/nginx/nginx.conf`。
- 为每个域名创建一个独立的配置文件，便于维护服务器。你可以按照需要定义任意多的 block 文件。
- Nginx 服务器配置文件被储存在`/etc/nginx/sites-available`目录下。在`/etc/nginx/sites-enabled`目录下的配置文件都将被 Nginx 使用。
- 最佳推荐是使用标准的命名方式。例如，如果你的域名是`mydomain.com`，那么配置文件应该被命名为`/etc/nginx/sites-available/mydomain.com.conf`
- 如果你在域名服务器配置块中有可重用的配置段，把这些配置段摘出来，做成一小段可重用的配置。
- Nginx 日志文件(access.log 和 error.log)定位在`/var/log/nginx/`目录下。推荐为每个服务器配置块，配置一个不同的`access`和`error`。

启动是可能报错：

```shell
nginx: [alert] could not open error log file: open() "/var/log/nginx/error.log" failed (13: Permission denied)
```

原因是没有访问该文件的权限，设置权限即可：

```shell
sudo chmod 777 /var/log/nginx/error.log
```

直接将/var/log/nginx路径修改权限也可

常见权限意义：

-rw------- (600) 只有所有者才有读和写的权限
-rw-r–r-- (644) 只有所有者才有读和写的权限，组群和其他人只有读的权限
-rwx------ (700) 只有所有者才有读，写，执行的权限
-rwxr-xr-x (755) 只有所有者才有读，写，执行的权限，组群和其他人只有读和执行的权限
-rwx–x--x (711) 只有所有者才有读，写，执行的权限，组群和其他人只有执行的权限
-rw-rw-rw- (666) 每个人都有读写的权限
-rwxrwxrwx (777) 每个人都有读写和执行的权限

### 将前端项目部署到nginx：

解压资料中的nginx-1.18.0压缩包，复制

```shell
./html/hdmp
```

文件夹，即前端项目，粘贴到自己项目路径，我的是：

```shell
/mnt/windows_D/data/java/redis-hmdp/hmdp
```

然后配置nginx

1.备份配置文件：

```shell
cd /etc/nginx
cp nginx.conf nginx.conf.bak
```

编辑配置文件nginx.conf，使用前面压缩包里面的nginx.conf，略作修改后替代：

```shell
sudo vim ./nginx.conf
```

关键：将项目的根目录所在路径作为 location / 的 root 对应的值

```yaml

worker_processes  1;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/json;

    sendfile        on;
    
    keepalive_timeout  65;

    server {
        listen       8080;
        server_name  localhost;
        # 指定前端项目所在的位置
        location / {
            root   /mnt/windows_D/data/java/redis-hmdp/hmdp;
            index  index.html index.htm;
        }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }


        location /api {  
            default_type  application/json;
            #internal;  
            keepalive_timeout   30s;  
            keepalive_requests  1000;  
            #支持keep-alive  
            proxy_http_version 1.1;  
            rewrite /api(/.*) $1 break;  
            proxy_pass_request_headers on;
            #more_clear_input_headers Accept-Encoding;  
            proxy_next_upstream error timeout;  
            proxy_pass http://127.0.0.1:8081;
            #proxy_pass http://backend;
        }
    }

    upstream backend {
        server 127.0.0.1:8081 max_fails=5 fail_timeout=10s weight=1;
        #server 127.0.0.1:8082 max_fails=5 fail_timeout=10s weight=1;
    }  
}

```

保存退出

检查配置较，重新加载配置，重启nginx：

```shell
nginx -t 
nginx -s reload
service nginx restart
```

启动后，访问http://127.0.0.1:8080 

