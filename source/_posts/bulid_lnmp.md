---
title: 搭建lnmp
date: 2017-09-20
---
lnmp
<!-- more -->
### 搭建nginx静态服务器
使用 yum 安装 Nginx：
``` bash
yum install nginx -y
```

修改 /etc/nginx/conf.d/default.conf，去除对 IPv6 地址的监听
，可参考下面的代码示例：

>CentOS 6 不支持 IPv6，需要取消对 IPv6 地址的监听，否则 Nginx 不能成功启动

``` bash
server {
    listen       80 default_server;
    # listen       [::]:80 default_server;
    server_name  _;
    root         /usr/share/nginx/html;

    # Load configuration files for the default server block.
    include /etc/nginx/default.d/*.conf;

    location / {
    }

    error_page 404 /404.html;
        location = /40x.html {
    }

    error_page 500 502 503 504 /50x.html;
        location = /50x.html {
    }

}
```

修改完成后，启动 Nginx：
``` bash
nginx
```

将 Nginx 设置为开机自动启动：

``` bash
chkconfig nginx on
```

### 安装 MySQL 数据库服务 ###

>CentOS7带有MariaDB而不是MySQL，MariaDB和MySQL一样也是开元的数据库，您可以使用yum -y install mariadb-server mariadb命令安装

使用 yum 安装 MySQL：
``` bash
yum install mysql-server -y
```

安装完成后，启动 MySQL 服务：
``` bash
service mysqld restart
```

设置 MySQL 账户 root 密码：
``` bash
/usr/bin/mysqladmin -u root password 'tMiOskMW'
```

将 MySQL 设置为开机自动启动：
``` bash
chkconfig mysqld on
```

### 搭建 PHP 环境 ###
使用 yum 安装 PHP：
``` bash
yum install php php-fpm php-mysql -y
```

安装之后，启动 PHP-FPM 进程：
``` bash
service php-fpm start
```

启动之后，可以使用下面的命令查看 PHP-FPM 进程监听哪个端口

>PHP-FPM 默认监听 9000 端口

``` bash
netstat -nlpt | grep php-fpm
```

把 PHP-FPM 也设置成开机自动启动：
``` bash
chkconfig php-fpm on
```

### 配置 Nginx 并运行 PHP 程序 ###
在 /etc/nginx/conf.d 目录中新建一个名为 php.conf 的文件，并配置 Nginx 端口 ，配置示例如下：
``` bash 
server {
    listen 8000;
    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    location ~ .php$ {
        root           /usr/share/php;
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }
}
```

修改配置完成后，重启 nginx 服务
``` bash
service nginx restart
```

这时候，我们就可以在/usr/share/php 目录下新建一个 info.php 文件来检查 php 是否安装成功了
