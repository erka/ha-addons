# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM=ghcr.io/home-assistant/aarch64-base:latest
ARG BUILD_VERSION=v0.0.1

FROM alpine:latest AS builder
ARG BUILD_VERSION=v0.0.1
RUN wget -q -O /tmp/exporter.tar.gz https://github.com/erka/sagemcom_fast_exporter/releases/download/${BUILD_VERSION}/sagemcom-fast-exporter-linux-arm64.tar.gz && \
  tar -xzf /tmp/exporter.tar.gz -C /tmp && \
  mv /tmp/sagemcom-fast-exporter /sagemcom-fast-exporter && \
  rm /tmp/exporter.tar.gz

FROM $BUILD_FROM

ENV USER=nobody

COPY --from=builder /sagemcom-fast-exporter /sagemcom-fast-exporter
RUN chmod a+x /sagemcom-fast-exporter

COPY start-exporter /start-exporter
RUN chmod a+x /start-exporter

CMD [ "/start-exporter" ]
