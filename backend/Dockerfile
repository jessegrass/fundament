# syntax=docker/dockerfile:1
ARG PLONE_VERSION=6.1.4
FROM plone/server-builder:${PLONE_VERSION} AS builder

ENV EXTRA_PACKAGES="relstorage==4.1.1 psycopg2==2.9.11 python-ldap==3.4.4 ZEO"

WORKDIR /app


# Add local code
COPY scripts/ scripts/
COPY . src

# Install some system-level dependencies
RUN apt-get update && apt-get install -y \
    libpq-dev \
    gcc

RUN bin/pip install psycopg2-binary

# Install local requirements and pre-compile mo files
RUN <<EOT
    set -e
    bin/pip install mxdev uv
    sed -i 's/-e .\[test\]/./g' src/mx.ini
    cd /app/src
    # remove potentially existing virtualenv from local build
    rm -rf .venv
    ../bin/mxdev -c mx.ini 
    ../bin/uv pip install -r requirements-mxdev.txt
    ../bin/python /compile_mo.py
EOT

FROM plone/server-prod-config:${PLONE_VERSION}

LABEL maintainer="Kai-Oli <kai@link-f.org>" \
      org.label-schema.name="fundament-backend" \
      org.label-schema.description="Fundament backend image." \
      org.label-schema.vendor="Kai-Oli"

# Copy /app from builder
COPY --from=builder /app /app

RUN <<EOT
    set -e
    ln -s /data /app/var
EOT
