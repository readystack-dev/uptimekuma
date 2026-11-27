# GENERATED L-009 hermetic Node build (--network=none, SBOM+SLSA-attestation-producing).
# Pinned base from BASE_IMAGE_DIGESTS.lock; vendored resolved /app tree + debs from Dockerfile.vendor.
# NO install verb offline — the fully-resolved, prod-pruned node_modules is COPYd verbatim.
FROM ubuntu:24.04@sha256:9c7f200c07e3d4a03e7249d2c16bf66a51120fb876aa2242cf31451412543289 AS nodedist
COPY vendored/node/ /nodedist/
RUN cd /nodedist && echo 'c54118104acc524633b5abe106bbf44a53126ec8b4e5fa105cb92b5d7de8a1a1  node-v22.23.5-linux-x64.tar.gz' | sha256sum -c - && \
    mkdir -p /opt/node && tar -xzf node-v22.23.5-linux-x64.tar.gz -C /opt/node --strip-components=1 --no-same-owner && \
    mkdir -p /opt/node/share/doc/nodejs && mv /opt/node/LICENSE /opt/node/share/doc/nodejs/LICENSE && \
    rm -rf /opt/node/CHANGELOG.md /opt/node/README.md /opt/node/lib/node_modules/npm /opt/node/lib/node_modules/corepack /opt/node/bin/npm /opt/node/bin/npx /opt/node/bin/corepack
FROM ubuntu:24.04@sha256:9c7f200c07e3d4a03e7249d2c16bf66a51120fb876aa2242cf31451412543289
ENV DEBIAN_FRONTEND=noninteractive NODE_ENV=production UPTIME_KUMA_IS_CONTAINER=1 DATA_DIR=/app/data UPTIME_KUMA_HOST=0.0.0.0 UPTIME_KUMA_PORT=3001
RUN --mount=type=bind,source=vendored/debs,target=/tmp/debs \
    set --; for f in /tmp/debs/*.deb; do [ -e "$f" ] && set -- "$@" "$f"; done; \
    for pass in 1 2 3 4 5; do [ $# -eq 0 ] || dpkg -i --skip-same-version "$@" >/dev/null 2>&1 && break; done; \
    dpkg --configure -a && bad= && for d in "$@"; do p=$(dpkg-deb -f "$d" Package) v=$(dpkg-deb -f "$d" Version); \
      case "$(dpkg-query -W -f='${Version} ${db:Status-Abbrev}' "$p" 2>/dev/null)" in "$v ii"*) ;; *) bad="$bad $p=$v" ;; esac; done && \
    { [ -z "$bad" ] || { echo "vendored debs not installed at their vendored version:$bad" >&2; false; }; } && \
    rm -rf /var/lib/apt/lists/* \
           /var/log/dpkg.log /var/log/alternatives.log /var/log/apt /var/cache/ldconfig/aux-cache /var/cache/fontconfig
COPY --from=nodedist /opt/node/ /usr/local/
ARG SOURCE_DATE_EPOCH=1795672796
RUN node --version && groupadd -r uptimekuma && useradd -r -g uptimekuma -d /app -m uptimekuma && \
    : "${SOURCE_DATE_EPOCH:?SOURCE_DATE_EPOCH must be set for a reproducible build}" && \
    sed -ri "s/^([^:]*:[^:]*):[0-9]*:/\1:$((SOURCE_DATE_EPOCH/86400)):/" /etc/shadow && \
    rm -f /etc/passwd- /etc/shadow- /etc/group- /etc/gshadow-
COPY --chown=uptimekuma:uptimekuma vendored/uptimekuma-src/ /app/
RUN mkdir -p /app/data && chown -R uptimekuma:uptimekuma /app/data
LABEL org.opencontainers.image.title="Uptime Kuma"
LABEL org.opencontainers.image.source="https://github.com/readystack-dev/uptimekuma"
LABEL org.opencontainers.image.licenses="MIT"
LABEL org.opencontainers.image.version="2.5.12-CE-ubuntu24.04-r4"
LABEL org.opencontainers.image.description="Uptime Kuma monitors service availability and sends alerts when outages occur. This self-contained application tracks status without requiring external databases or complex infrastructure."
LABEL org.opencontainers.image.revision="5aa5dec425f8a955b54e150636979a6927745ec5"
LABEL readystack.upstream.source="https://github.com/louislam/uptime-kuma"
LABEL org.opencontainers.image.url="https://readystack.dev/products/uptimekuma"
LABEL org.opencontainers.image.documentation="https://github.com/readystack-dev/uptimekuma#readme"
LABEL org.opencontainers.image.authors="ReadyStack <contact@readystack.dev>"
LABEL org.opencontainers.image.vendor="ReadyStack.dev"
HEALTHCHECK --interval=5s --timeout=120s --start-period=20s \
  CMD curl -fsS -o /dev/null -w '%{http_code}' http://127.0.0.1:3001/api/entry-page || exit 1
USER uptimekuma
WORKDIR /app
EXPOSE 3001
ENTRYPOINT ["/usr/bin/dumb-init", "--", "node", "server/server.js"]
