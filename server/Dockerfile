FROM kylemanna/openvpn:latest

LABEL maintainer="Mauro Iorio <iorio.mauro@gmail.com>"

# Edge repo will not update out of the box
RUN set -ue && \
    cp /etc/apk/repositories /etc/apk/repositories.bak && \
    sed -e 's/^.*edge.*$//g' -i /etc/apk/repositories
RUN set -ue && \
    apk update && \
    apk upgrade --no-cache

# Re-enable edge and update again
RUN set -ue && \
    mv /etc/apk/repositories.bak /etc/apk/repositories
RUN set -ue && \
    apk update && \
    apk upgrade --no-cache

ADD docker-entrypoint.sh /docker-entrypoint.sh

ENTRYPOINT [ "/docker-entrypoint.sh" ]
