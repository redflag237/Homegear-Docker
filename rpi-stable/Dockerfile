FROM arm32v7/debian:stretch
MAINTAINER Sathya Laufer <sathya@homegear.email>
COPY qemu-arm-static /usr/bin/qemu-arm-static
RUN apt-get update && apt-get -y install apt-transport-https wget ca-certificates apt-utils gnupg libzip4 libavahi-client3 libavahi-client-dev insserv
RUN \
    touch /tmp/HOMEGEAR_STATIC_INSTALLATION; \
    wget https://apt.homegear.eu/Release.key && apt-key add Release.key && rm Release.key; \
    echo 'deb https://apt.homegear.eu/Debian/ stretch/' >> /etc/apt/sources.list.d/homegear.list; \
    apt-get update && apt-get -y install homegear homegear-management homegear-webssh homegear-adminui homegear-nodes-core homegear-nodes-extra homegear-homematicbidcos homegear-homematicwired homegear-insteon homegear-max homegear-philipshue homegear-sonos homegear-kodi homegear-ipcam homegear-beckhoff homegear-knx homegear-enocean homegear-intertechno homegear-zwave homegear-mbus homegear-ccu homegear-influxdb; \
    rm -f /etc/homegear/dh1024.pem; \
    rm -f /etc/homegear/homegear.crt; \
    rm -f /etc/homegear/homegear.key; \
    cp -R /etc/homegear /etc/homegear.config; \
    cp -R /var/lib/homegear /var/lib/homegear.data; \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

VOLUME ["/etc/homegear", "/var/lib/homegear", "/var/log/homegear"]

COPY start.sh /start.sh
RUN chmod +x /start.sh
ENTRYPOINT ["/bin/bash", "-c", "/start.sh"]

EXPOSE 2001 2002 2003
