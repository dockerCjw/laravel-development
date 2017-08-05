FROM ubuntu:16.04
MAINTAINER chenjiawen <604989282@qq.com>

# 第一步 更换阿里镜像apt源
COPY ./sources.list /etc/apt/sources.list

# 第二步 安装程序
RUN apt-get update \
    && apt-get -y install openssh-server vim git wget unzip \
    && apt-get -y install php php-mysql php-curl php-dom php-mbstring \
    # ifconfig ping 两个命令
    && apt-get -y install net-tools iputils-ping

# 第三步 复制 composer
COPY ./composer.phar /usr/local/bin/composer
RUN chmod 777 /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://packagist.phpcomposer.com

# 第四步 生成 密钥对 
RUN ssh-keygen -t rsa -f /root/.ssh/id_rsa

VOLUME  /var/www

EXPOSE 22

CMD ["/etc/init.d/ssh", "start","-D"]
