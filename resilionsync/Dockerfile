ARG BUILD_FROM
FROM ${BUILD_FROM}

#docker run -d   --name=resilio-sync -e UMASK=022  -e PUID=1000   -e PGID=100   -e TZ=Asia/Singapore   -p 8888:8888   -p 55555:55555   -v /usr/share/rsync:/config   -v /usr/share/rsync/downloads:/downloads   -v /media/nashdd/:/sync   --restart unless-stopped   ghcr.io/linuxserver/resilio-sync
#docker pull ghcr.io/linuxserver/resilio-sync:version-2.7.2.1375@sha256:ccc80929245d8051f8964918dfeaf2617cfa4e9e3d257e4095ef6b9b6aaaadf4

# Copy root filesystem
COPY root /

#RUN apt-get update \
# && DEBIAN_FRONTEND=noninteractive apt-get install -y jq smbclient \
# && apt-get clean \
# && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* ~/.cache
#
## Change the root folder for Nextcloud to the /share directory to be persistent
#RUN  sed -i "s|/var/www|/share/nextcloud|g" /etc/apache2/sites-enabled/000-default.conf \
#  && sed -i "s|/var/www|/share/nextcloud|g" /etc/apache2/apache2.conf \
#  && sed -i "s|/var/www/html|/share/nextcloud/html|g" /entrypoint.sh \
#  && sed -i "s|/var/www/html|/share/nextcloud/html|g" /usr/src/nextcloud/config/autoconfig.php
#
#RUN echo "ServerName localhost" | tee /etc/apache2/conf-available/fqdn.conf && a2enconf fqdn

ENTRYPOINT [ "/usr/bin/run.sh" ]
CMD ["apache2-foreground"]

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION


