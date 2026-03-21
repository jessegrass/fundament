# syntax=docker/dockerfile:1
FROM varnish:7.6

LABEL maintainer="Kai-Oli <kai@link-f.org>" \
      org.label-schema.name="Fundament-varnish" \
      org.label-schema.description="Fundament Varnish image." \
      org.label-schema.vendor="Kai-Oli"

COPY etc/varnish.vcl /etc/varnish/default.vcl
