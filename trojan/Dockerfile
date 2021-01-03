FROM arm64v8/alpine

ARG TROJAN_SERVER_HOST
ARG TROJAN_SERVER_PORT
ARG TROJAN_PASSWORD

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk update \
    && apk add --no-cache --allow-untrusted --virtual .build-deps \
        build-base \
        cmake \
        boost-dev \
        openssl-dev \
        mariadb-connector-c-dev \
        git \
        jq \
    && ( \
        git clone --depth 1 https://github.com/trojan-gfw/trojan && cd trojan \
            && cmake . \
            && make -j $(nproc) \
            && strip -s trojan \
            && make install \
            && mkdir -p /etc/trojan \
            && cat examples/client.json-example \
                | jq ".remote_addr|=\"${TROJAN_SERVER_HOST}\"" \
                | jq ".remote_port|=\"${TROJAN_SERVER_PORT}\"" \
                | jq ".password[0]|=\"${TROJAN_PASSWORD}\"" \
                | jq ".local_port|=\"1080\"" \
                | jq ".local_addr|=\"0.0.0.0\"" > /etc/trojan/client.json \
            && cd .. \
            && rm -rf trojan \
       ) \
    && apk del .build-deps \
    && apk add --no-cache --allow-untrusted --virtual .trojan-rundeps \
        libstdc++ \
        boost-system \
        boost-program_options \
        mariadb-connector-c

CMD [ "/usr/local/bin/trojan", "-l", "/dev/stdout", "/etc/trojan/client.json" ]
