# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.195.0/containers/javascript-node/.devcontainer/base.Dockerfile
# [Choice] Node.js version (use -bullseye variants on local arm64/Apple Silicon): 16, 14, 12, 16-bullseye, 14-bullseye, 12-bullseye, 16-buster, 14-buster, 12-buster
ARG VARIANT=14-bullseye
FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:0-${VARIANT}

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

LABEL maintainer="toomore_such <info(at)webgent.com>"

ENV LANG C.UTF-8
ENV DEBCONF_NOWARNINGS yes
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -qq && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends build-essential && \
    apt-get install -y --no-install-recommends libglu1-mesa libglu1 libxi6 libgconf-2-4 && \
    #libglu1-mesa-glx
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# [Optional] Uncomment if you want to install an additional version of node using nvm
# ARG EXTRA_NODE_VERSION=10
# RUN su node -c "umask 0002 && ./usr/local/share/nvm/nvm.sh && nvm install ${EXTRA_NODE_VERSION}"

# [Optional] Uncomment if you want to install more global node modules
# RUN su node -c "npm install -g <your-package-list-here>"

# ELM & EJS
RUN npm install -g --unsafe-perm=true --no-optional \
    ejs-cli \
    html-minify

# NCU & IMAGEMIN
RUN npm install -g --unsafe-perm=true \
    npm-check-updates \
    imagemin-cli \
    imagemin-gifsicle \
    imagemin-keep-folder \
    imagemin-mozjpeg \
    imagemin-pngquant

# ELM
# RUN npm install -g --unsafe-perm=true \
# elm \
# elm-format \
# elm-live \
# elm-test \

# GATSBY
RUN npm install -g --unsafe-perm=true \
    gatsby-cli

RUN npm cache clean --force
RUN gatsby telemetry --disable

WORKDIR /tmp

ARG USER="node"
RUN mkdir -p apps && \
    chown -R ${USER}:${USER} apps

USER ${USER}
RUN echo 'alias nl="npm list --depth=0"' >> ~/.bashrc
RUN echo 'alias nlg="npm list --depth=0 -g"' >> ~/.bashrc
RUN echo 'alias gatsby-server="gatsby develop -p 80 --host 0.0.0.0"' >> ~/.bashrc
