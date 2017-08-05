FROM node:6.11.2
MAINTAINER chenjiawen <604989282@qq.com>

ENV WORKSPACE /var

WORKDIR $WORKSPACE/

RUN npm install -g express-generator@4 \
    && express ./node \
    && cd node \
    && npm install

EXPOSE 3000

CMD ["node","./node/bin/www"]
