# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/master/containers/ruby
# [Choice] Ruby version: 3, 3.1, 3.0, 2, 2.7, 2.6, 3-bullseye, 3.1-bullseye, 3.0-bullseye, 2-bullseye, 2.7-bullseye, 2.6-bullseye, 3-buster, 3.1-buster, 3.0-buster, 2-buster, 2.7-buster, 2.6-buster
ARG VARIANT=2.6-bullseye
FROM mcr.microsoft.com/vscode/devcontainers/ruby:0-${VARIANT}

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

LABEL maintainer="toomore_such <info(at)webgent.com>"

ENV LANG C.UTF-8
ENV DEBCONF_NOWARNINGS yes
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -qq && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends build-essential libpq-dev nodejs sqlite3 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# [Optional] Uncomment if you want to install an additional version of node using nvm
# ARG EXTRA_NODE_VERSION=10
# RUN su node -c "umask 0002 && ./usr/local/share/nvm/nvm.sh && nvm install ${EXTRA_NODE_VERSION}"

# [Optional] Uncomment if you want to install more global node modules
# RUN su node -c "npm install -g <your-package-list-here>"

RUN echo 'gem: --no-document' > /etc/gemrc && \
    gem install bundler

WORKDIR /tmp

ARG USER="vscode"
RUN mkdir -p apps && \
    chown -R ${USER}:${USER} apps

USER ${USER}
RUN echo 'alias middleman-server="bundle exec middleman -p 80"' >> ~/.bashrc
RUN echo 'alias middleman-build="bundle exec middleman build --verbose || bundle exec middleman build --verbose"' >> ~/.bashrc
