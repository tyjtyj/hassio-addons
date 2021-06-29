ARG BUILD_FROM
ARG BUILD_VERSION
ARG BUILD_UPSTREAM="2.7.2.1375-ls90"
FROM ${BUILD_FROM}${BUILD_UPSTREAM}
#docker run -d   --name=resilio-sync -e UMASK=022  -e PUID=1000   -e PGID=100   -e TZ=Asia/Singapore   -p 8888:8888   -p 55555:55555   -v /usr/share/rsync:/config   -v /usr/share/rsync/downloads:/downloads   -v /media/nashdd/:/sync   --restart unless-stopped   ghcr.io/linuxserver/resilio-sync
#docker pull ghcr.io/linuxserver/resilio-sync:version-2.7.2.1375@sha256:ccc80929245d8051f8964918dfeaf2617cfa4e9e3d257e4095ef6b9b6aaaadf4

# Add bashio
RUN apk add --no-cache \
    curl \
    jq \
    && curl -J -L -o /tmp/bashio.tar.gz \
    "https://github.com/hassio-addons/bashio/archive/v0.13.0.tar.gz" \
    && mkdir /tmp/bashio \
    && tar zxvf \
    /tmp/bashio.tar.gz \
    --strip 1 -C /tmp/bashio \
    \
    && mv /tmp/bashio/lib /usr/lib/bashio \
    && ln -s /usr/lib/bashio/bashio /usr/bin/bashio \
    && rm -fr /tmp/bashio.tar.gz

# Copy root filesystem
COPY rootfs /

# MOFIFY DATA PATH
#RUN sed -i "s|config|config/resilio-sync|g" /etc/services.d/resilio-sync/run \
#    && sed -i "s|config|config/resilio-sync|g" /etc/cont-init.d/20-config \
#    # Allow UID and GID setting
#    && sed -i 's/bash/bashio/g' /etc/cont-init.d/10-adduser \
#    && sed -i 's/{PUID:-911}/(bashio::config "PUID")/g' /etc/cont-init.d/10-adduser \
#    && sed -i 's/{PGID:-911}/(bashio::config "PGID")/g' /etc/cont-init.d/10-adduser

VOLUME [ "/data" ]

### LABELS
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="tyjtyj (https://github.com/tyjtyj)" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant Add-ons" \
    org.opencontainers.image.authors="tyjtyj (https://github.com/tyjtyj)" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://github.com/tyjtyj" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
