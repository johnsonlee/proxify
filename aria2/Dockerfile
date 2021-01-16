FROM arm64v8/alpine

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk add --update --allow-untrusted aria2

COPY ./aria2.conf /etc/aria2/aria2.conf

VOLUME /data/downloads

EXPOSE 6800

CMD [ "/usr/bin/aria2c", "--dir=/data/downloads/", "--conf-path=/etc/aria2/aria2.conf" ]
