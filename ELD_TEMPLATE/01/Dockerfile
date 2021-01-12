# SEE also:
# * https://github.com/colindensem/luckyframework-sandbox/blob/alpine-support/.devcontainer/Dockerfile
# * https://github.com/luckyframework-docker/
# * https://github.com/luckyframework/lucky/issues/1255 re 'lsof procps'

ARG VARIANT=0.35.1
FROM crystallang/crystal:${VARIANT}-alpine

RUN apk update && apk upgrade \
    && echo @latest-stable http://nl.alpinelinux.org/alpine/latest-stable/community >> /etc/apk/repositories \
    && echo @latest-stable http://nl.alpinelinux.org/alpine/latest-stable/main >> /etc/apk/repositories \
    && apk add --no-cache gnupg tmux bash postgresql-client nodejs yarn openssh \
    chromium-chromedriver@latest-stable chromium@latest-stable lsof procps

RUN cd /tmp \
    && git clone https://github.com/luckyframework/lucky_cli \
    && cd lucky_cli \
    && git checkout v0.25.0 \
    && shards install \
    && crystal build src/lucky.cr \
    && mv lucky /usr/local/bin \
    && rm -rf /tmp/luckly_cli \
    && cd /tmp \
    && wget https://github.com/DarthSim/overmind/releases/download/v2.2.0/overmind-v2.2.0-linux-amd64.gz \
    && gunzip -d overmind-v2.2.0-linux-amd64.gz \
    && chmod a+x overmind-v2.2.0-linux-amd64 \
    && mv overmind-v2.2.0-linux-amd64 /usr/local/bin/overmind

# Clean up leftovers.
RUN rm -rf /var/cache/apk/* \
    /tmp/*

# Set the environment variables for the Chromium browser.
ENV CHROME_BIN=/usr/bin/chromium-browser \
    CHROME_PATH=/usr/lib/chromium/

# My app:
WORKDIR /app
ADD . /app

# Optionally, add `--ignore-crystal-version` to end of `shards install` and `shards update`
RUN shards install
RUN shards update

# RUN script/setup
# RUN shards build
