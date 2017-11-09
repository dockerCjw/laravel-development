FROM ubuntu:16.04
MAINTAINER chenjiawen <604989282@qq.com>

# 第一步 更换阿里镜像apt源
COPY ./sources-ali.list /etc/apt/sources.list

# 第二步 安装php
RUN apt-get update \
    && apt-get -y install php7.0 \
    && apt-get -y install php7.0-fpm php-mysql php-curl php-dom php-mbstring php-gd php-zip

# 第三步 安装mongodb 扩展 （可以删去）
COPY ./sources-official.list /etc/apt/sources.list
RUN apt-get update \
    && apt-get -y install php-pear \
    && apt-get -y install php-dev \
    && apt-get -y install libpcre3-dev \
    && apt-get -y install openssl \
    && ln -s /usr/lib/x86_64-linux-gnu/libssl.so  /usr/lib \
    && pecl install mongodb

RUN echo 'extension=mongodb.so' | tee /etc/php/7.0/mods-available/mongodb.ini

RUN ln -s /etc/php/7.0/mods-available/mongodb.ini /etc/php/7.0/fpm/conf.d/ \
    && ln -s /etc/php/7.0/mods-available/mongodb.ini /etc/php/7.0/cli/conf.d/

COPY ./sources-ali.list /etc/apt/sources.list

# 第三步 开启php的扩展
# 覆盖 php-fpm文件 ，1. 关闭 pid 配置 （ 第17行 ）  2. 关闭守护进程  （ 第82行）
COPY  ./php-fpm.conf /etc/php/7.0/fpm/php-fpm.conf

# 覆盖 www.conf文件 1. 修改listen = [::]:9000 （ 第 36 行）
COPY  ./pool.d /etc/php/7.0/fpm/pool.d

# 添加 php.ini 配置信息
COPY  ./conf.d /etc/php/7.0/fpm/conf.d

EXPOSE 9000
CMD ["php-fpm7.0"]
