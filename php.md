# Debian下搭建php开发环境
安装nginx、php

```
# apt update
# apt install nginx-extras php php-fpm 
```

卸载多余的apache
```
# apt purge apache2 && apt autoremove --purge
```

安装php依赖管理器
```
# apt install composer
```

执行以下命令来使用composer中国源
```
$ composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

安装laravel需要的php扩展
```
# apt install php-zip php-mbstring php-xml
```

查看当前安装的php扩展，确保安装了laravel需要的openssl、pdo、xml、zip、tokenizer扩展。
```
$ php -m
```

安装laravel
```
$ composer global require "laravel/installer"
```

修改PATH变量使之包含可执行文件laravel所在的目录。
```
echo 'export PATH=$PATH:$HOME/.config/composer/vendor/bin' >> ~/.zshrc
```

安装mariadb
```
# apt install mariadb-server mariadb-client
```

初始化mariadb
```
# mysql_secure_installation
```