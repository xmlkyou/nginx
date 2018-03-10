# nginx
nginx 安装配置
一  准备工作
1. 确定linux内核未2.6及以上   uname -a
2. 安装gcc，g++，yum install -y gcc；yum install -y gcc-c++ ，检查是否已经安装:rpm -qa|grep -i gcc
3. 安装PCRE（正则表达式，nginx.confg中使用），yum install -y pcre pcre-devel
4. 安装zlib库, yum install -y zlib zlib-devel(二次开发需要的库)
5. 安装OpenSSL库, yum install -y openssl openssl-devel

二  磁盘目录
1. 源码目录，包括nginx源码，以及自己所写模块
2. 编译产生的中间文件
3. 部署目录，存放可执行程序与配置文件
4. 日志目录

三 linux内核参数优化，/etc/sysctl.conf （此部分需注意）
1. file-max  进程同时打开的句柄数
2. tcp_max_syn_backlog TCP三次握手阶段，SYN请求队列长度
3. tcp_syncookies  与性能无关，用于解决tcp的syn攻击

四 编译安装nginx
1. 下载安装包
2. ./configure,  ./configure --help 查看参数
  1）默认安装路径为 /usr/local/nginx, sbin:可执行程序 conf:配置文件 logs:日志，master进行id，lock文件
  2）--with-pcre 强制使用pcre；--with-openssl
   示例:./configure  --sbin-path=/usr/local/nginx/nginx --conf-path=/usr/local/nginx/nginx.conf --pid-path=/usr/local/nginx/nginx.pid --with-http_ssl_module --with-pcre=/usr/local/src/pcre-8.39 --with-zlib=/usr/local/src/zlib-1.2.8 --with-openssl=/usr/local/src/openssl-1.1.0c
3. make
4. make install
//未验证
./configure --with-zlib=/usr/local/src/zlib-1.2.8

 + using system PCRE library 
 + OpenSSL library is not used 
 + using zlib library: /usr/local/src/zlib-1.2.8
 
 prce、zlib默认安装， 需要指定zlib源文件

问题：
1） 403，permission denied ：查询error.log文件，资源路径上面的文件夹 是否有读权限，  worker进程以nobody运行，不需要进行修改
2)  当访问目录时，nginx会发送301重定向，url末尾会加上/，  但是好像非目录有时也会重定向，尚需实验
