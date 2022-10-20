FROM buildpack-deps:stretch

# taken from https://stackoverflow.com/questions/67680726/installing-haskells-cabal-or-ghcup-inside-a-dockerfile-wont-work

ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Europe/Berlin

RUN \
    apt-get update -y && \
    apt-get install -y --no-install-recommends \
        curl \
        libnuma-dev \
        zlib1g-dev \
        libgmp-dev \
        libgmp10 \
        git \
        wget \
        lsb-release \
        software-properties-common \
        gnupg2 \
        apt-transport-https \
        gcc \
        autoconf \
        automake \
        build-essential

ARG GPG_KEY=7784930957807690A66EBDBE3786C5262ECB4A3F
RUN gpg --batch --keyserver keys.openpgp.org --recv-keys $GPG_KEY

RUN \
    curl https://downloads.haskell.org/~ghcup/x86_64-linux-ghcup > /usr/bin/ghcup && \
    chmod +x /usr/bin/ghcup && \
    ghcup config set gpg-setting GPGStrict

ARG GHC=9.2.4
ARG CABAL=3.8.1.0
ARG STACk=2.9.1

RUN \
    ghcup -v install ghc --isolate /usr/local --force ${GHC} && \
    ghcup -v install cabal --isolate /usr/local/bin --force ${CABAL} && \
    ghcup -v install stack --isolate /usr/local/bin --force ${STACK}