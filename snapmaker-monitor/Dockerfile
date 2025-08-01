ARG BUILD_FROM=ghcr.io/hassio-addons/base:18.0.3
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
# Copy Python requirements file
COPY requirements.txt /tmp/

# Setup base
# hadolint ignore=DL3042
RUN \
  apk add --no-cache --virtual .build-dependencies \
  build-base=0.5-r3 \
  py3-pip=25.1.1-r0 \
  python3-dev=3.12.11-r0 \
  \
  && apk add --no-cache \
  python3=3.12.11-r0 \
  \
  && pip3 install -r /tmp/requirements.txt \
  \
  && apk del --no-cache --purge .build-dependencies

# Copy root filesystem
COPY rootfs /

WORKDIR /data

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
  io.hass.name="${BUILD_NAME}" \
  io.hass.description="${BUILD_DESCRIPTION}" \
  io.hass.arch="${BUILD_ARCH}" \
  io.hass.type="addon" \
  io.hass.version=${BUILD_VERSION} \
  maintainer="Steven 'NemesisRE' Kurz <nemesissre@gmail.com>" \
  org.opencontainers.image.title="${BUILD_NAME}" \
  org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
  org.opencontainers.image.vendor="Home Assistant Community Add-ons" \
  org.opencontainers.image.authors="Steven 'NemesisRE' Kurz <nemesissre@gmail.com>" \
  org.opencontainers.image.licenses="MIT" \
  org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
  org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
  org.opencontainers.image.created=${BUILD_DATE} \
  org.opencontainers.image.revision=${BUILD_REF} \
  org.opencontainers.image.version=${BUILD_VERSION}
