# Proxify

A proxy service based on trojan & privoxy, support both `SOCK5` and `HTTP(S)` protocols.

## Getting Started

```bash
git clone https://github.com/johnsonlee/proxify.git
cd proxify && docker-compose up -d \
    -e TROJAN_SERVER_HOST=xxx \
    -e TROJAN_SERVER_PORT=xxx \
    -e TROJAN_PASSWORD=xxx
```

