FROM alpine:latest

ARG VERSION

COPY start /

RUN apk add --no-cache --update samba=4.10.5-r0 && \
  chmod 755 /start && \
  addgroup -g 2000 samba && \
  adduser -S -h /config -s /bin/false -u 2000 -G samba samba

EXPOSE 137/udp 138/udp 139 445

CMD ["/start"]

VOLUME ["/run/samba", "/var/cache"]

HEALTHCHECK --interval=200s --timeout=15s \
  CMD smbclient -L '\\\\localhost\\' -U 'guest%' -m SMB3

LABEL org.label-schema.name="Samba" \
  org.label-schema.version=4.10.5-r0 \
  org.label-schema.docker.schema-version="1.0"