安装lamp
```
# apt install nginx-extra php php-fpm 
```

安装php依赖管理器
```
# apt install composer
```

执行以下命令来使用composer中国源
```
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

安装laravel需要的php扩展
```
# apt install php-zip php-mbstring php-xml
```

查看当前安装的php扩展，确保安装了laravel需要的openssl、pdo、xml、zip、tokenizer扩展。
```
php -m
```

安装laravel
```
composer global require "laravel/installer"
```

修改PATH变量使之包含可执行文件laravel所在的目录。