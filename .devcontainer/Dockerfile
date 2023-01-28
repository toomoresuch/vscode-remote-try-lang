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

RUN apt-get update -qq && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends bubblewrap darcs m4 mercurial opam rlwrap && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /usr/share/doc /usr/share/man


# [Optional] Uncomment if you want to install an additional version of node using nvm
# ARG EXTRA_NODE_VERSION=10
# RUN su node -c "umask 0002 && ./usr/local/share/nvm/nvm.sh && nvm install ${EXTRA_NODE_VERSION}"

# [Optional] Uncomment if you want to install more global node modules
# RUN su node -c "npm install -g <your-package-list-here>"

WORKDIR /tmp

ARG USER="vscode"
RUN mkdir -p apps && \
    chown -R ${USER}:${USER} apps

USER ${USER}

# [Opam init in Dockerfile · Issue \#4327 · ocaml/opam](https://github.com/ocaml/opam/issues/4327)
# RUN opam update
RUN opam init -y --disable-sandboxing
RUN opam pin -y add ocaml-lsp-server https://github.com/ocaml/ocaml-lsp.git
RUN opam install -y base core_kernel dune merlin ocaml-lsp-server ocamlformat ounit qcheck
RUN echo 'eval $(opam env)' >> ~/.bashrc

#〈mk2/ocaml-dev-workspace〉
# https://github.com/mk2/ocaml-dev-workspace

#〈johnnymn/ocaml-devcontainer: OCaml development environment for VSCode〉
# https://github.com/johnnymn/ocaml-devcontainer
