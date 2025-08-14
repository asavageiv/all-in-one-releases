# syntax=docker/dockerfile:latest
# From https://github.com/docker-library/redis/blob/master/7.2/alpine/Dockerfile
FROM redis:7.2.10-alpine

COPY --chmod=775 /Containers/redis/start.sh /start.sh
COPY --chmod=775 /Containers/redis/healthcheck.sh /healthcheck.sh

RUN set -ex; \
    apk upgrade --no-cache -a; \
    apk add --no-cache openssl bash; \
    \
# Give root a random password
    echo "root:$(openssl rand -base64 12)" | chpasswd; \
    \
# Get rid of unused binaries
    rm -f /usr/local/bin/gosu;


USER 999
ENTRYPOINT ["/start.sh"]

HEALTHCHECK CMD /healthcheck.sh
LABEL com.centurylinklabs.watchtower.enable="false" \
    org.label-schema.vendor="Nextcloud"
