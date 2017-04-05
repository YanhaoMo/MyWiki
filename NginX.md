# 安装
debian上的nginx有三个版本，不同版本之间的差异可以在[这儿](https://wiki.debian.org/Nginx)找到。

```
apt update && apt install nginx-extra
```

# 安装php
```
apt install php php-fpm
```

# 配置

```
server {
    listen 80 default_server;
    root /var/www;
    index index.php index.html;
    server_name example.com;
    location / {
        try_files $uri $uri/ = 404;
    }
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
    }
}
```