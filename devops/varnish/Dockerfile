# syntax=docker/dockerfile:1
FROM varnish:7.6

LABEL maintainer="Kai-Oli <kai@link-f.org>" \
      org.label-schema.name="clasic-varnish" \
      org.label-schema.description="clasic Varnish image." \
      org.label-schema.vendor="Kai-Oli"

COPY etc/varnish.vcl /etc/varnish/default.vcl
