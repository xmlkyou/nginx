# nginx
nginx 安装配置
一  准备工作
1. 确定linux内核未2.6及以上   uname -a
2. 安装gcc，g++，yum install -y gcc；yum install -y gcc-c++ ，检查是否已经安装:npm -qa|grep -i gcc
3. 安装PCRE（正则表达式，nginx.confg中使用），yum install -y pcre pcre-devel
4. 安装zlib库, yum install -y zlib zlib-devel(二次开发需要的库)
5. 安装OpenSSL库, yum install -y openssl openssl-devel

