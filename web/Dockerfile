ARG JITSI_REPO=jitsi
FROM ${JITSI_REPO}/base

ADD https://raw.githubusercontent.com/acmesh-official/acme.sh/2.8.8/acme.sh /opt
COPY rootfs/ /

RUN \
	apt-dpkg-wrap apt-get update && \
	apt-dpkg-wrap apt-get install -y cron nginx-extras jitsi-meet-web socat && \
	apt-dpkg-wrap apt-get -d install -y jitsi-meet-web-config && \
    dpkg -x /var/cache/apt/archives/jitsi-meet-web-config*.deb /tmp/pkg && \
    mv /tmp/pkg/usr/share/jitsi-meet-web-config/config.js /defaults && \
	mv /usr/share/jitsi-meet/interface_config.js /defaults && \
	rm -f /etc/nginx/conf.d/default.conf && \
	apt-cleanup && \
	rm -rf /tmp/pkg /var/cache/apt

EXPOSE 80 443

COPY ./customfiles/main-enGB.json /usr/share/jitsi-meet/lang/main-enGB.json
COPY ./customfiles/title.html /usr/share/jitsi-meet/title.html
COPY ./customfiles/images /usr/share/jitsi-meet/images
COPY ./customfiles/all.css /usr/share/jitsi-meet/css/all.css

VOLUME ["/config", "/usr/share/jitsi-meet/transcripts"]
