FROM alpine:latest

RUN apk add --no-cache curl \
    && ARCH=$(uname -m) \
    && if [ "${ARCH}" = "i386" ]; then ARCH="386"; fi \
    && if [ "${ARCH}" = "i686" ]; then ARCH="386"; fi \
    && if [ "${ARCH}" = "x86_64" ]; then ARCH="amd64"; fi \
    && if [ "${ARCH}" = "aarch64" ]; then ARCH="arm64"; fi \
    && WIREPROXY_URL=$(curl -fsSL https://api.github.com/repos/artem-russkikh/wireproxy-awg/releases/latest | grep 'browser_download_url' | cut -d'"' -f4 | grep "wireproxy_linux_${ARCH}.tar.gz") \
    && curl -fsSL "${WIREPROXY_URL}" -o ./wireproxy.tar.gz \
    && tar -xzf wireproxy.tar.gz \
    && rm wireproxy.tar.gz \
    && chmod +x ./wireproxy \
    && mv ./wireproxy /usr/bin

VOLUME [ "/etc/wireproxy"]
ENTRYPOINT [ "/usr/bin/wireproxy" ]
CMD [ "--config", "/etc/wireproxy/config" ]

LABEL org.opencontainers.image.title="wireproxy-awg"
LABEL org.opencontainers.image.description="AmneziaWG client that exposes itself as a socks5 proxy"
LABEL org.opencontainers.image.licenses="ISC"
