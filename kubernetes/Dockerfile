FROM mcr.microsoft.com/vscode/devcontainers/base:alpine

ARG SKAFFOLD_VERSION=1.36.0
ARG KUBERNETES_VERSION=1.23.4
ARG HELM_VERSION=3.7.1

RUN apk add --update docker openrc gettext bash curl git make
RUN rc-update add docker boot
RUN LOOKUP=`uname -m` && \
    if [ "$LOOKUP" == "x86_64" ]; then \
       ARCH="amd64"; \
    elif [ "$LOOKUP" == "aarch64" ]; then \
       ARCH="arm64"; \
    fi; \
    curl -L "https://storage.googleapis.com/skaffold/releases/v$SKAFFOLD_VERSION/skaffold-linux-$ARCH" -o /usr/local/bin/skaffold && \
    curl -L "https://dl.k8s.io/release/v$KUBERNETES_VERSION/bin/linux/$ARCH/kubectl" -o /usr/local/bin/kubectl && \
    curl -L "https://get.helm.sh/helm-v$HELM_VERSION-linux-$ARCH.tar.gz" -o - | tar zxv --strip-components 1 -C /usr/local/bin -f - linux-$ARCH/helm

RUN chmod +x /usr/local/bin/*

WORKDIR /opt/workspace

CMD [ "sleep", "infinity" ]
