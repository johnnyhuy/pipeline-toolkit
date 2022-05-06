FROM mcr.microsoft.com/vscode/devcontainers/base:alpine

ARG NODE_VERSION=16.13.2
ARG NVM_VERSION=0.39.1
ARG DOCKER_COMPOSE_VERSION=2.2.3

# NVM
ENV NVM_DIR=/root/.nvm
ENV PATH="$PATH:$HOME/.local/bin:$HOME/bin:$NVM_DIR/versions/node/v$NODE_VERSION/bin"
RUN curl -Lo- https://raw.githubusercontent.com/nvm-sh/nvm/v$NVM_VERSION/install.sh | bash && \
    . "$NVM_DIR/nvm.sh" && \
    nvm install $NODE_VERSION

# Docker
ENV DOCKER_CONFIG=$HOME/.docker
RUN apk add --update docker openrc gettext bash curl git make && \
    rc-update add docker boot && \
    mkdir -p $DOCKER_CONFIG/cli-plugins && \

# Install tools
RUN LOOKUP=`uname -m` && if [ "$LOOKUP" == "x86_64" ]; then ARCH="amd64"; elif [ "$LOOKUP" == "aarch64" ]; then ARCH="arm64"; fi; \
    curl -L "https://storage.googleapis.com/skaffold/releases/v$SKAFFOLD_VERSION/skaffold-linux-$ARCH" -o /usr/local/bin/skaffold && \
    curl -L "https://dl.k8s.io/release/v$KUBERNETES_VERSION/bin/linux/$ARCH/kubectl" -o /usr/local/bin/kubectl && \
    curl -L "https://get.helm.sh/helm-v$HELM_VERSION-linux-$ARCH.tar.gz" -o - | tar zxv --strip-components 1 -C /usr/local/bin -f - linux-$ARCH/helm && \
    curl -SL https://github.com/docker/compose/releases/download/v${DOCKER_COMPOSE_VERSION}/docker-compose-linux-$ARCH -o $DOCKER_CONFIG/cli-plugins/docker-compose && chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose

WORKDIR /opt/workspace

USER root

CMD [ "sleep", "infinity" ]
