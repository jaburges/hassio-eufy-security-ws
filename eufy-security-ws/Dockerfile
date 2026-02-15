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

# Install patched eufy-security-client: use CMD_START_REALTIME_MEDIA direct for T85V0 + WebRTC detection
# Remove nested copy so eufy-security-ws uses our patched top-level version
COPY eufy-security-client-3.7.5.tgz /tmp/eufy-security-client-3.7.5.tgz
RUN npm install --force /tmp/eufy-security-client-3.7.5.tgz \
    && rm -rf /usr/src/app/node_modules/eufy-security-ws/node_modules/eufy-security-client \
    && rm /tmp/eufy-security-client-3.7.5.tgz

COPY run.sh /
RUN chmod a+x /run.sh
WORKDIR /data

CMD [ "/run.sh" ]