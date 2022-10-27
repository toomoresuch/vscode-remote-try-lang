# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/master/containers/debian
# [Choice] Debian version: 11, 10, 9
ARG VARIANT=11
FROM mcr.microsoft.com/vscode/devcontainers/base:0-debian${VARIANT}

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

LABEL maintainer="toomore_such <info(at)webgent.com>"

ENV LANG C.UTF-8
ENV DEBCONF_NOWARNINGS yes
ENV DEBIAN_FRONTEND noninteractive

ARG GHC="8.10.4"
ARG CABAL_INSTALL="3.4"
ARG STACK="2.5.1"

# [Debian Instructions](https://downloads.haskell.org/~debian/)
# [haskell/docker\-haskell](https://github.com/haskell/docker-haskell)
RUN echo 'deb http://downloads.haskell.org/debian bullseye main' > /etc/apt/sources.list.d/ghc.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys BA3CBA3FFE22B574 && \
    apt-get update -qq && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends cabal-install-${CABAL_INSTALL} ghc-${GHC} haskell-stack && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# [Optional] Uncomment if you want to install an additional version of node using nvm
# ARG EXTRA_NODE_VERSION=10
# RUN su node -c "umask 0002 && ./usr/local/share/nvm/nvm.sh && nvm install ${EXTRA_NODE_VERSION}"

# [Optional] Uncomment if you want to install more global node modules
# RUN su node -c "npm install -g <your-package-list-here>"

RUN update-alternatives --config opt-cabal && \
    update-alternatives --config opt-ghc && \
    yes | stack upgrade && \
    echo "########## Upgrade was done! ##########" && \
    stack config set system-ghc --global true && \
    stack config set install-ghc --global false

WORKDIR /tmp

ARG USER="vscode"
RUN mkdir -p apps && \
    chown -R ${USER}:${USER} apps

USER ${USER}
RUN stack setup && \
    stack install implicit-hie

ENV PATH /opt/cabal/${CABAL_INSTALL}/bin:/opt/ghc/${GHC}/bin:$PATH

CMD ["ghci"]
# RUN echo function stacknew() {command stack new $1 && cd $1 && gen-hie > hie.yaml} >> ~/.bashrc
