ARG BUILD_FROM
FROM $BUILD_FROM

ARG BUILD_ARCH
ARG BUILD_VERSION

LABEL maintainer "Ben Figlin <secret@email.com>"

RUN case $(arch) in \
        x86_64|amd64) export ARCH=x86_64 ;; \
        i386) export ARCH=i386 ;; \
        armv6l|armv7l) export ARCH=armv6l ;; \
        aarch64) export ARCH=aarch64 ;; \
    esac && \
    apt-get update && \
    apt-get install -y git && \
    git clone https://github.com/benfiglin/fliclib-linux-hci /tmp/src && \
    cp /tmp/src/bin/${ARCH}/flicd /usr/bin/flicd && \
    chmod +x /usr/bin/flicd && \
    mkdir /config && \
    rm -rf /tmp/src && \
    apt-get remove --purge -y git && \
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /data
VOLUME ["/data"]
EXPOSE 5551
ENTRYPOINT ["/usr/bin/flicd"]
CMD ["-f", "/data/flic-db", "-s", "0.0.0.0", "-p", "5551"]
