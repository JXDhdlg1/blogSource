---
title: linux下安装nginx_mysql_php
date: 2016-01-01 15:41:23
tags: [linux,php,nginx,mysql]
categories: php
---
本文分享下安装lnmp环境的详细步骤。
欢迎讨论和吐槽。

### 简单说明
- 本文是基于Centos 7，于命令行下安装php7+nginx+mysql;
- 其中php+nginx的安装步骤来自我的好朋友以及是我的前公司开发组组长的分享（很帅技术很强），亲测ok；
- mysql的安装是基于网上的博客分享。
### php+nginx安装
```$xslt
yum update --skip-broken
//安装相关依赖库
yum -y install php-mcrypt libmcrypt libmcrypt-devel libxml2-devel openssl-devel libcurl-devel libjpeg.x86_64 libpng.x86_64 freetype.x86_64 libjpeg-devel.x86_64 libpng-devel.x86_64 freetype-devel.x86_64 libjpeg-turbo-devel libmcrypt-devel mysql-devel libicu-devel glibc-headers libxslt-devel gcc-c++ pcre-devel
mkdir ~/Soft && cd Soft
wget http://jaist.dl.sourceforge.net/project/mcrypt/Libmcrypt/2.5.8/libmcrypt-2.5.8.tar.gz
tar zxvf libmcrypt-2.5.8.tar.gz
cd libmcrypt-2.5.8
./configure
make && make install
cd ..
//卸载预装PHP
yum remove php
rpm -qa | grep php | xargs rpm -e
// 编译安装PHP7.0.9
wget http://cn2.php.net/distributions/php-7.0.9.tar.gz
tar zxvf php-7.0.9.tar.gz
cd php-7.0.9
./configure --prefix=/usr/local/php --with-config-file-path=/etc/php --enable-fpm --with-fpm-user=webid --with-fpm-group=webid --enable-mysqlnd --with-mysqli=mysqlnd --with-pdo-mysql=mysqlnd --with-iconv-dir --with-freetype-dir=/usr/local/freetype --with-jpeg-dir --with-png-dir --with-zlib --with-libxml-dir=/usr --enable-xml --disable-rpath --enable-bcmath --enable-shmop --enable-sysvsem --enable-inline-optimization --with-curl --enable-mbregex --enable-mbstring --enable-intl --enable-pcntl --with-mcrypt --enable-ftp --with-gd --enable-gd-native-ttf --with-openssl --with-mhash --enable-pcntl --enable-sockets --with-xmlrpc --enable-zip --enable-soap --with-gettext --disable-fileinfo --enable-opcache --with-xsl --enable-sysvmsg --with-imap-ssl
make && make install
// 建立软连接
ln -s /usr/local/php/bin/php /usr/bin/php
mkdir /etc/php
cp php.ini-production /etc/php/php.ini
cp sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm
chmod +x /etc/init.d/php-fpm
cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf
groupadd webid
useradd -s /sbin/nologin -g webid webid
cp /usr/local/php/etc/php-fpm.d/www.conf.default /usr/local/php/etc/php-fpm.d/www.conf
cd ..
// 安装redis扩展
wget -c https://github.com/phpredis/phpredis/archive/php7.zip
unzip php7.zip
cd phpredis-php7/
/usr/local/php/bin/phpize
//执行上一步如果出现“Cannot find autoconf”，则需要执行
yum install m4
yum install autoconf
/usr/local/php/bin/phpize
./configure --with-php-config=/usr/local/php/bin/php-config
make && make install
cd ..
// vim /etc/php/php.ini
// extension=redis.so
service php-fpm restart
// 安装swoole扩展
wget -c https://github.com/swoole/swoole-src/archive/1.8.7-stable.tar.gz
tar zxvf 1.8.7-stable.tar.gz
cd swoole-src-1.8.7-stable/
/usr/local/php/bin/phpize
./configure --with-php-config=/usr/local/php/bin/php-config
make && make install
cd ..
// vim /etc/php/php.ini
// extension=swoole.so
service php-fpm restart
//安装nginx
wget http://nginx.org/download/nginx-1.10.1.tar.gz
tar zxvf nginx-1.10.1.tar.gz
cd nginx-1.10.1
./configure --user=webid --group=webid --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module --with-http_v2_module --with-http_gzip_static_module --with-ipv6 --with-http_sub_module
make && make install
cd ..
ln -s /usr/local/nginx/sbin/nginx /usr/sbin/nginx
ln -s /usr/local/nginx/conf /etc/nginx
mkdir /usr/local/nginx/conf/vhost
// 配置优化
vim /usr/local/php/etc/php-fpm.d/www.conf
listen = /dev/shm/php7.sock
chown webid:webid /dev/shm/php7.sock
// 开机启动
chmod +x /etc/init.d/php-fpm
chkconfig --add /etc/init.d/php-fpm
chkconfig php-fpm on
// 创建文件 /etc/init.d/nginx
chmod +x /etc/init.d/nginx
chkconfig --add /etc/init.d/nginx
chkconfig nginx on
mkdir -p /data/logs/www/nginx
mkdir -p /data/webserver
passenger + nginx 安装(Centos 7)
yum install -y epel-release yum-utils
yum-config-manager --enable epel
sudo yum install -y pygpgme curl
sudo curl --fail -sSLo /etc/yum.repos.d/passenger.repo https://oss-binaries.phusionpassenger.com/yum/definitions/el-passenger.repo
yum install -y nginx passenger
systemctl start nginx.service
gitlab install (centos 7 )
yum install curl policycoreutils openssh-server openssh-clients
systemctl enable sshd
systemctl start sshd
yum install postfix
systemctl enable postfix
systemctl start postfix
firewall-cmd --permanent --add-service=http
systemctl reload firewalld
curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
sudo yum install gitlab-ce
gitlab-ctl reconfigure
```

### mysql安装
可以参考这个教程，步骤比较详细：[安装mysql](http://www.cnblogs.com/fnlingnzb-learner/p/5830622.html)

### 写在最后
我在刚开始搭建环境的时候遇到过问题，基本网上一搜都能找到答案；
自己使用推荐的php+nginx安装命令是安装成功的。