FROM arm64v8/httpd:alpine

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk update \
    && apk add --no-cache --allow-untrusted --virtual .webui-aria2 git \
    && git clone --depth 1 https://github.com/ziahamza/webui-aria2 \
    && mkdir -p /usr/local/apache2/htdocs/ \
    && cp -rvf webui-aria2/docs/* /usr/local/apache2/htdocs/ \
    && rm -rf webui-aria2 \
    && apk del .webui-aria2

