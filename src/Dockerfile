FROM alpine:3.4

MAINTAINER takafumiotake<tikutaka.dev@gmail.com>

RUN S6_VERSION=v1.18.1.5 \
    && apk add --update --no-cache --virtual .verify-deps \
        gnupg \
        curl \
    && curl -fSL https://github.com/just-containers/s6-overlay/releases/download/$S6_VERSION/s6-overlay-amd64.tar.gz -o s6-overlay.tar.gz \
    && curl -fSL https://github.com/just-containers/s6-overlay/releases/download/$S6_VERSION/s6-overlay-amd64.tar.gz.sig -o s6-overlay.tar.gz.sig \
    && export GNUPGHOME="$(mktemp -d)" \
    && curl -fSL https://keybase.io/justcontainers/key.asc | gpg --import \
    && gpg --batch --verify s6-overlay.tar.gz.sig s6-overlay.tar.gz \
    && rm -rf $GNUPGHOME s6-overlay.tar.gz.sig \
    && tar -xzC / -f s6-overlay.tar.gz \
    && rm -f s6-overlay.tar.gz \
    && apk del .verify-deps

ENTRYPOINT ["/init"]
