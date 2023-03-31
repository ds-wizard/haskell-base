FROM ubuntu:22.04

ARG TARGET_ARCH
ARG STACK_VERSION=2.9.3
ARG GHC_VERSION=9.4.4
ARG RESOLVER=nightly-2023-03-05

ENV LANG=C.UTF-8 \
    LC_ALL=C.UTF-8 \
    PATH="/root/.local/bin:$PATH"

RUN apt-get update \
 && apt-get -q -yy install wget netbase ca-certificates g++ gcc jq pkg-config \ 
                           libc6-dev libffi-dev libgmp-dev zlib1g-dev libtinfo-dev  \
                           liblzma-dev libpq-dev make xz-utils build-essential \
 && rm -rf /var/lib/apt/lists/*

RUN ARCH="$(dpkg-architecture --query DEB_BUILD_GNU_CPU)"; \
    STACK_URL="https://github.com/commercialhaskell/stack/releases/download/v${STACK_VERSION}/stack-${STACK_VERSION}-linux-${ARCH}.tar.gz"; \
    wget -qO- $STACK_URL | tar xz --wildcards --strip-components=1 -C /usr/bin '*/stack';

RUN mkdir /etc/stack/ && echo "system-ghc: true" >/etc/stack/config.yaml

RUN stack setup --resolver $RESOLVER
