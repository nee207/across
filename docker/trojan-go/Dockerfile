# Dockerfile for trojan-go based alpine
# Copyright (C) 2019 - 2024 Teddysun <i@teddysun.com>
# Reference URL:
# https://github.com/p4gefau1t/trojan-go
# https://github.com/v2fly/v2ray-core
# https://github.com/v2fly/geoip
# https://github.com/v2fly/domain-list-community

FROM alpine:latest
LABEL maintainer="Teddysun <i@teddysun.com>"

COPY trojan-go.sh /root/trojan-go.sh
COPY config.json /etc/trojan-go/config.json
RUN set -ex \
	&& apk add --no-cache tzdata ca-certificates \
	&& chmod +x /root/trojan-go.sh \
	&& /root/trojan-go.sh \
	&& rm -fv /root/trojan-go.sh \
	&& mkdir -p /usr/share/trojan-go \
	&& wget -O /usr/share/trojan-go/geosite.dat https://github.com/v2fly/domain-list-community/releases/latest/download/dlc.dat \
	&& wget -O /usr/share/trojan-go/geoip.dat https://github.com/v2fly/geoip/releases/latest/download/geoip.dat \
	&& wget -O /usr/share/trojan-go/geoip-only-cn-private.dat https://github.com/v2fly/geoip/releases/latest/download/geoip-only-cn-private.dat \
	&& ln -fs /usr/share/trojan-go/geoip.dat /usr/bin/ \
	&& ln -fs /usr/share/trojan-go/geoip-only-cn-private.dat /usr/bin/ \
	&& ln -fs /usr/share/trojan-go/geosite.dat /usr/bin/ 

VOLUME /etc/trojan-go
ENV TZ=Asia/Shanghai
CMD [ "/usr/bin/trojan-go", "-config", "/etc/trojan-go/config.json" ]
