FROM ghcr.io/siderolabs/talosctl:v1.7.4 AS talosctl
FROM docker.io/mikefarah/yq:4.44.1 AS yq
FROM mcr.microsoft.com/devcontainers/python:3.12
COPY --from=talosctl /talosctl /usr/local/bin/talosctl
COPY --from=yq /usr/bin/yq /usr/local/bin/yq

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        python3-pip \
        libssl-dev \
        libonig-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
