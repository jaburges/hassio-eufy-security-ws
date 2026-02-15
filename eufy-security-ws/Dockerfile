ARG BUILD_FROM
FROM $BUILD_FROM

ARG EUFY_SECURITY_WS_VERSION

WORKDIR /usr/src/app
RUN \
    set -x \
    && apk add --no-cache \
    nodejs \
    npm \
    jq \
    && npm install --force \
    "eufy-security-ws@${EUFY_SECURITY_WS_VERSION}"

# Install patched eufy-security-client with T85V0 support and diagnostic logging
COPY eufy-security-client-3.7.0.tgz /tmp/eufy-security-client-3.7.0.tgz
RUN npm install --force /tmp/eufy-security-client-3.7.0.tgz \
    && rm /tmp/eufy-security-client-3.7.0.tgz

COPY run.sh /
RUN chmod a+x /run.sh
WORKDIR /data

CMD [ "/run.sh" ]