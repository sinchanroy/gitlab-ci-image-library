FROM google/cloud-sdk:alpine

LABEL maintainer="sinchanroy4890@gmail.com"

ENV SPRUCE_VERSION=1.29.0
ENV HELM_VERSION=3.9.2
ENV RELEASE_ROOT="https://get.helm.sh"
ENV RELEASE_FILE="helm-v${HELM_VERSION}-linux-amd64.tar.gz"

# Installing terraform
RUN apk add unzip wget curl --no-cache && \
    cd /tmp && \
    curl -o /tmp/terraform.zip https://releases.hashicorp.com/terraform/1.2.6/terraform_1.2.6_linux_amd64.zip && \
    unzip /tmp/terraform.zip && \
    cp /tmp/terraform /usr/local/bin && \
    chmod a+x /usr/local/bin/terraform && \
    wget https://github.com/geofffranks/spruce/releases/download/v${SPRUCE_VERSION}/spruce-linux-amd64 && \
    chmod +x spruce-linux-amd64 && \
    mv spruce-linux-amd64 /usr/local/bin/spruce && \
    curl -L ${RELEASE_ROOT}/${RELEASE_FILE} | tar xvz && \
    mv linux-amd64/helm /usr/bin/helm && \
    chmod +x /usr/bin/helm && \
    curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.24.3/bin/linux/amd64/kubectl && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/bin/kubectl && \
    apk del unzip wget curl && \
    rm /tmp/terraform /tmp/terraform.zip
