# Base Image
FROM debian:buster

WORKDIR /usr/src/app
WORKDIR /usr/tmp

# Install general tools requirements
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    apt-utils \
    apt-transport-https \
    bash \
    bash-completion \
    coreutils \
    ca-certificates \
    curl \
    file \
    git \
    gnupg2 \
    libc6 \
    libc6-dev \
    libgpgme11-dev \
    libdevmapper1.02.1 \
    jq \
    make \
    openssl \
    python \
    python-dev \
    python3-pip \
    python3-setuptools \
    software-properties-common \
    tar \
    unzip \
    vim \
    && rm -rf /var/lib/apt/lists/*

RUN ln -s /lib/x86_64-linux-gnu/libdevmapper.so.1.02.1 /usr/lib/libdevmapper.so.1.02

# Tools and Versions
ENV TERRAFORM_VERSION 0.12.7
ENV HELM_VERSION=v2.16.0
ENV DIVE_VERSION=0.9.0
ENV KUBE_BENCH_VERSION=0.1.0
ENV KUBE_SCORE_VERSION=1.3.0
ENV KUBE_AUDIT_VERSION=0.7.0
ENV AUDIT_RBAC_VERSION=0.7.0
ENV KUBE_BOX_VERSION=0.6.1

# Setup Kubernetes and Docker APT
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
RUN echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list
RUN  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - 
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"

# Install docker cli, kubernetes, kubeadm
RUN apt-get update && \
    apt-get install -y docker-ce-cli kubectl kubeadm --no-install-recommends

# Install Docker Compose
RUN pip3 install docker-compose

# Install terraform
RUN curl -LO https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip
RUN unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip && mv terraform /usr/local/bin

# Install Helm
RUN curl -L https://git.io/get_helm.sh | bash -s -- -v ${HELM_VERSION}

# Install Dive Container Analysis Tool
RUN curl -LO https://github.com/wagoodman/dive/releases/download/v${DIVE_VERSION}/dive_${DIVE_VERSION}_linux_amd64.tar.gz
RUN tar xvf ./dive_${DIVE_VERSION}_linux_amd64.tar.gz && mv dive /usr/local/bin

# Install Kube Bench
RUN curl -LO https://github.com/aquasecurity/kube-bench/releases/download/v${KUBE_BENCH_VERSION}/kube-bench_${KUBE_BENCH_VERSION}_linux_amd64.tar.gz
RUN tar xvf ./kube-bench_${KUBE_BENCH_VERSION}_linux_amd64.tar.gz && mv kube-bench /usr/local/bin
RUN curl -LO https://github.com/aquasecurity/kube-bench/archive/v${KUBE_BENCH_VERSION}.zip
RUN unzip v${KUBE_BENCH_VERSION}.zip && mv kube-bench-${KUBE_BENCH_VERSION}/cfg /usr/src/app/cfg


# Install Kube Score
RUN curl -LO https://github.com/zegl/kube-score/releases/download/v${KUBE_SCORE_VERSION}/kube-score_${KUBE_SCORE_VERSION}_linux_amd64.tar.gz
RUN tar xvf ./kube-score_${KUBE_SCORE_VERSION}_linux_amd64.tar.gz && mv kube-score /usr/local/bin

# Install Kube Audit
RUN curl -LO https://github.com/Shopify/kubeaudit/releases/download/v${KUBE_AUDIT_VERSION}/kubeaudit_${KUBE_AUDIT_VERSION}_linux_amd64.tar.gz
RUN tar xvf ./kubeaudit_${KUBE_AUDIT_VERSION}_linux_amd64.tar.gz && mv kubeaudit /usr/local/bin

# Install Kops
RUN curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
RUN chmod +x kops-linux-amd64
RUN mv kops-linux-amd64 /usr/local/bin/kops

# Install Audit2RBAC
RUN curl -LO https://github.com/liggitt/audit2rbac/releases/download/v${AUDIT_RBAC_VERSION}/audit2rbac-linux-amd64.tar.gz

# Install KubeBox
RUN curl -Lo kubebox https://github.com/astefanutti/kubebox/releases/download/v${KUBE_BOX_VERSION}/kubebox-linux
RUN chmod +x kubebox && mv kubebox /usr/local/bin/kubebox

# Install 
RUN curl -Lo hadolint https://github.com/hadolint/hadolint/releases/download/v1.17.2/hadolint-Linux-x86_64
RUN chmod +x hadolint && mv hadolint /usr/local/bin/hadolint

RUN rm -Rf /usr/tmp
RUN rm -rf /var/lib/apt/lists/*

WORKDIR /usr/src/app

# Install kube-shell
RUN pip3 install kube-shell

ENTRYPOINT [ "kube-shell" ]