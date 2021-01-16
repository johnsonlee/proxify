FROM arm64v8/alpine

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk add --update --allow-untrusted privoxy

EXPOSE 1081

CMD [ "/usr/sbin/privoxy", "--no-daemon", "/etc/privoxy/config" ]
