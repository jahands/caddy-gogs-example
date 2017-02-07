FROM alpine:3.4
MAINTAINER Jacob Hands <jacob@gogit.io>

RUN apk --no-cache add tini git \
    && apk --no-cache add --virtual devs tar curl

#Install Caddy Server, and All Middleware
RUN curl "https://caddyserver.com/download/build?os=linux&arch=amd64&features=" \
    | tar --no-same-owner -C /usr/bin/ -xz caddy

# Remove build devs
RUN apk del devs

#Copy over Caddyfile
COPY ./Caddyfile /etc/Caddyfile

RUN mkdir /var/caddy_files

# VOLUME ["/var/caddy_files"]

ENTRYPOINT ["/sbin/tini"]

CMD ["caddy", "-conf=/etc/Caddyfile", "-agree=true", "-log=stdout", "-root=/var/tmp", "-email=jacob@gogit.io"]
