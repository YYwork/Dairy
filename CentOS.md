## `CentOS` 下安装`PHP` 环境

CentOS 开发环境

PHP
MySQL
Nginx
Redis
Apache
Vim
Git
Python
Ruby


[CentOS 下安装 PHP 环境](http://www.jxtobo.com/62657.html)
[phpMyAdmin 安装](http://down.chinaz.com/server/201202/1660_1.htm)
[CentOS 6源码安装GitLab](http://www.centoscn.com/image-text/install/2015/0320/4929.html)
[Centos 安装 NodeJS](http://www.laozuo.org/6421.html)


[apache报Permission denied](http://blog.sina.com.cn/s/blog_7e56997901016bw7.html)
[centOS 启用中文输入法](http://jingyan.baidu.com/article/da1091fb3e7f8a027849d681.html)

### `yum`源更换为国内的阿里云源

第一步：备份你的原镜像文件，以免出错后可以恢复。
```bash
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```
第二步：下载新的`CentOS-Base.repo` 到`/etc/yum.repos.d/`

CentOS 5
```bash
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-5.repo
```

CentOS 6
```bash
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
```
第三步：运行`yum makecache`生成缓存
```
yum clean all
yum makecache
```

### 启动`ssh`服务，更新`yum`源

```
service sshd start
yum -y update
```

### 安装`PHP`

```
yum install php55w  php55w-bcmath php55w-cli php55w-common php55w-devel php55w-fpm    php55w-gd php55w-imap  php55w-ldap php55w-mbstring php55w-mcrypt php55w-mysql   php55w-odbc   php55w-pdo php55w-pear  php55w-pecl-igbinary  php55w-xml php55w-xmlrpc php55w-opcache php55w-intl php55w-pecl-memcache
```
```
whereis php
```
启动php-fpm
```bash
/etc/rc.d/init.d/php-fpm start
```

### 安装`Redis`服务器
```bash
> yum install wget make gcc gcc-c++ zlib-devel openssl openssl-devel pcre-devel kernel keyutils patch perl
> 
> mkdir /tmp/redis
> 
> cd /tmp/redis
> 
> wget http://download.redis.io/releases/redis-2.8.8.tar.gz
> 
> tar xzf redis-*
> 
> cd redis-*
> 
> make
> 
> sudo make install clean
> 
> mkdir /etc/redis
> 
> cp redis.conf /etc/redis/redis.conf
```

```
vim /etc/redis/redis.conf
```


```
daemonize yes
port 6379
bind 127.0.0.1
dir /var/opt
```

查看是否安装成功
```bash
> whereis redis-server
> 
> /usr/local/bin/redis-server /etc/redis/redis.conf
>
>  redis-cli
```


### 安装 PHPRedis
下载地址
https://github.com/nicolasff/phpredis/archive/2.2.4.tar.gz

上传 `phpredis-2.2.4.tar.gz` 到 `/usr/local/src` 目录
```
> cd /usr/local/src
> 
> tar zxvf phpredis-2.2.4.tar.gz
> 
> cd phpredis-2.2.4
> 
> find / -name "phpize"
> 
> /usr/bin/phpize
> 
> whereis php
> 
> ./configure --with-php-config=/usr/bin/php-config
> 
> make
> 
> make install
> 
> vim /usr/bin/php.ini
```

### 安装`Nginx`

```
> yum install nginx -y
>
> /etc/init.d/nginx start
>
> /etc/nginx/nginx.conf
```


> 
> find / -name "phpize"

### 安装`MySQL`

```bash
yum install mysql mysql-server

chkconfig mysqld on

service mysqld start

mysql -uroot -p
```

---
[PHP]()
```
/etc/rc.d/init.d/php-fpm start
sudo vim /etc/php.ini
```
[Redis]()
```
redis-cli
```
[nginx](http://localhost/)
```
/usr/share/nginx/html
/etc/init.d/nginx start
```
[apache](http://localhost:56/)
```
/var/www/html/

vi /etc/httpd/conf/httpd.conf
/etc/init.d/httpd restart
```
[phpmyadmin](http://localhost:56/phpmyadmin/)
```
vi /etc/httpd/conf.d/phpmyadmin.conf
vi /usr/share/phpmyadmin/config.inc.php
```



主机与虚拟机互PING，但主机无法访问虚拟机服务解决
 
1.本机能ping通虚拟机
2.虚拟机也能ping通本机
3.虚拟机能访问自己的web
4.本机无法访问虚拟己的web 

后来发现是防火墙将80端口屏蔽了的缘故。
检查是不是服务器的80端口被防火墙堵了，可以通过命令：
telnet {服务器ip}80 来测试。 

解决方法如下：
/sbin/iptables -I INPUT -p tcp --dport 80 -j ACCEPT
然后保存
 /etc/rc.d/init.d/iptables save
 重启防火墙
 /etc/init.d/iptables restart 
 
CentOS防火墙的关闭，关闭其服务即可：
查看CentOS防火墙信息：
/etc/init.d/iptables status 
关闭CentOS防火墙服务：
/etc/init.d/iptables stop 
永久关闭防火墙：
chkconfig --level 35 iptables off 
最后，打开主机浏览器，输入虚拟机地方，就可以访问虚拟机的WEB服务器了




[root@localhost gitlab]# sudo -u git -H bundle exec rake gitlab:setup RAILS_ENV=production

[!] There was an error parsing `Gemfile`: compile error - syntax error, unexpected ':', expecting $end
gem "mysql2", group: :mysql
                    ^. Bundler cannot continue.

 #  from /home/git/gitlab/Gemfile:20
 #  -------------------------------------------
 #  # Supported DBs
 >  gem "mysql2", group: :mysql
 #  gem "pg", group: :postgres
 #  -------------------------------------------

https://ruby-china.org/wiki/rvm-guide

