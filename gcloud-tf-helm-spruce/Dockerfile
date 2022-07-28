FROM alpine:3.15.5

ENV TERRAFORM_VERSION=1.2.6
ENV SPRUCE_VERSION=1.29.0
ENV HELM_VERSION=3.9.2
ENV RELEASE_ROOT="https://get.helm.sh"
ENV RELEASE_FILE="helm-v${HELM_VERSION}-linux-amd64.tar.gz"
ENV KUBECTL_VERSION=1.24.3

# Installing terraform
RUN apk add unzip wget curl --no-cache && \
    cd /tmp && \
    curl -o /tmp/terraform.zip https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
    unzip /tmp/terraform.zip && \
    cp /tmp/terraform /usr/local/bin && \
    chmod a+x /usr/local/bin/terraform && \
    wget https://github.com/geofffranks/spruce/releases/download/v${SPRUCE_VERSION}/spruce-linux-amd64 && \
    chmod +x spruce-linux-amd64 && \
    mv spruce-linux-amd64 /usr/local/bin/spruce && \
    curl -L ${RELEASE_ROOT}/${RELEASE_FILE} | tar xvz && \
    mv linux-amd64/helm /usr/bin/helm && \
    chmod +x /usr/bin/helm && \
    curl -LO https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/bin/kubectl

FROM google/cloud-sdk:alpine

LABEL maintainer="sinchanroy4890@gmail.com"

COPY --from=0 /usr/local/bin/terraform /usr/local/bin/terraform
COPY --from=0 /usr/local/bin/spruce /usr/local/bin/spruce
COPY --from=0 /usr/bin/helm /usr/bin/helm
COPY --from=0 /usr/bin/kubectl /usr/bin/kubectl

