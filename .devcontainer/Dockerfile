FROM ghcr.io/siderolabs/talosctl:v1.7.5 AS talosctl
FROM docker.io/mikefarah/yq:4.44.1 AS yq
FROM mcr.microsoft.com/devcontainers/python:3.12
COPY --from=talosctl /talosctl /usr/local/bin/talosctl
COPY --from=yq /usr/bin/yq /usr/local/bin/yq
COPY requirements.txt /tmp/requirements.txt
COPY requirements.yml /tmp/requirements.yml
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        python3-pip \
        libssl-dev \
        libonig-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && pip install --no-cache-dir -r /tmp/requirements.txt \
    && ansible-galaxy install -r /tmp/requirements.yml \
    && rm -f /tmp/requirements.*
