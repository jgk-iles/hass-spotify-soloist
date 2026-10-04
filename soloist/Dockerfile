ARG BUILD_FROM=ghcr.io/hassio-addons/debian-base:9.5.0
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup base
# Spotify Soloist itself is NOT part of this image: Spotify does not allow it
# to be redistributed, so it is downloaded from Spotify at runtime. It loads
# libpulse at runtime to play through Home Assistant's audio server.
# pulseaudio-utils provides pactl for the debug-mode audio logging.
RUN \
    apt-get update \
    \
    && apt-get install -y --no-install-recommends \
        libatomic1=14.2.0-19 \
        libpulse0=17.0+dfsg1-2+b1 \
        pulseaudio-utils=17.0+dfsg1-2+b1 \
    \
    && apt-get clean \
    && rm -fr \
        /tmp/* \
        /var/lib/apt/lists/*

# Copy root filesystem
COPY rootfs /

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
    maintainer="Joseph Iles" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.authors="Joseph Iles" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
