FROM nginx:latest
MAINTAINER chenjiawen <604989282@qq.com>

# 第一步 切换工作目录
WORKDIR /etc/nginx

# 第二步 添加证书 和 主要的配置信息
COPY cert cert/
COPY conf.d conf.d

# 第三步 挂载站点数据卷
VOLUME /etc/nginx/sites-enabled
VOLUME /var/log/nginx

EXPOSE 80
EXPOSE 443

CMD ["nginx","-g","daemon off;"]
