FROM mcr.microsoft.com/vscode/devcontainers/typescript-node:0-16-bullseye

ARG NODE_VERSION=16.13.2
ARG NVM_VERSION=0.39.1
ARG DOCKER_COMPOSE_VERSION=2.2.3

# Install NVM
ENV NVM_DIR=/root/.nvm
ENV PATH="$PATH:$HOME/.local/bin:$HOME/bin:$NVM_DIR/versions/node/v$NODE_VERSION/bin"
RUN curl -Lo- https://raw.githubusercontent.com/nvm-sh/nvm/v$NVM_VERSION/install.sh | bash && \
    . "$NVM_DIR/nvm.sh" && \
    nvm install $NODE_VERSION

# Install Docker CLI and Docker Compose
ENV DOCKER_CONFIG=$HOME/.docker
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
        $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null && \
    apt-get update && export DEBIAN_FRONTEND=noninteractive && \
    apt-get -y install --no-install-recommends docker-ce-cli && \
    mkdir -p $DOCKER_CONFIG/cli-plugins && \
    curl -SL https://github.com/docker/compose/releases/download/v${DOCKER_COMPOSE_VERSION}/docker-compose-$(uname)-$(arch) -o $DOCKER_CONFIG/cli-plugins/docker-compose && \
    chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose

WORKDIR /opt/workspace

USER root

CMD [ "sleep", "infinity" ]
