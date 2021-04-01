ARG BUILD_FROM
FROM ${BUILD_FROM}

#docker run -d   --name=resilio-sync -e UMASK=022  -e PUID=1000   -e PGID=100   -e TZ=Asia/Singapore   -p 8888:8888   -p 55555:55555   -v /usr/share/rsync:/config   -v /usr/share/rsync/downloads:/downloads   -v /media/nashdd/:/sync   --restart unless-stopped   ghcr.io/linuxserver/resilio-sync
#docker pull ghcr.io/linuxserver/resilio-sync:version-2.7.2.1375@sha256:ccc80929245d8051f8964918dfeaf2617cfa4e9e3d257e4095ef6b9b6aaaadf4

# Copy root filesystem
COPY root /

RUN \
 echo "**** install resilio-sync ****" && \
 if [ -z ${SYNC_VERSION+x} ]; then \
	SYNC_VERSION=$(curl -sL https://help.resilio.com/hc/en-us/articles/206178924-Installing-Sync-package-on-Linux | awk -F '(download-cdn.resilio.com/|/Debian/)' '/x64/ {print $2}'); \
 fi && \
 curl -o \
 /tmp/sync.deb -L \
	"https://download-cdn.resilio.com/${SYNC_VERSION}/Debian/resilio-sync_${SYNC_VERSION}-1_arm64.deb" && \
 dpkg -i \
 /tmp/sync.deb && \
 echo "**** cleanup ****" && \
 rm -rf \
	/tmp/*

# add local files
COPY root/ /

# ports and volumes
EXPOSE 8888 55555
VOLUME /config /sync


