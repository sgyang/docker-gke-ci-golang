FROM golang:1.7

# docker
RUN apt-get update && apt-get install -y apt-transport-https ca-certificates gnupg2 \
    && apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D \
    && echo "deb https://apt.dockerproject.org/repo debian-jessie main" > /etc/apt/sources.list.d/docker.list \
    && apt-get update && apt-get install -y docker-engine

# gcloud
ENV GCLOUD_VERSION=138.0.0
RUN curl -o /tmp/gcloud.tar.gz https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${GCLOUD_VERSION}-linux-x86.tar.gz \
    && tar -C /usr/local -xvf /tmp/gcloud.tar.gz \
    && /usr/local/google-cloud-sdk/install.sh
ENV PATH /usr/local/google-cloud-sdk/bin/:$PATH

# kubectl
ENV KUBECTL_VERSION=1.4.7
RUN curl -o /usr/local/bin/kubectl https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl \
    && chmod +x /usr/local/bin/kubectl

# default crendentials settings
ENV GOOGLE_APPLICATION_CREDENTIALS /etc/key.json
