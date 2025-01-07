FROM ubuntu:22.04
ENV TARGETARCH="linux-x64"
# Also can be "linux-arm", "linux-arm64".

RUN apt update
RUN apt upgrade -y
RUN apt install -y curl git jq libicu70


RUN apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        jq \
        git \
        iputils-ping \
	libcurl4 \
        # libcurl3 \
        # libicu55 \
        # libicu60 \
        libunwind8 \
        netcat \
        zip \
        unzip \
        wget \
        apt-transport-https \
	gnupg \
        gnupg-agent \
        # software-properties-common \
        apt-utils

# To make it easier for build and release pipelines to run apt-get,
# configure apt to not require confirmation (assume the -y argument by default)
ENV DEBIAN_FRONTEND=noninteractive
RUN echo "APT::Get::Assume-Yes \"true\";" > /etc/apt/apt.conf.d/90assumeyes

# Install helm v3 (latest)
#RUN curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 \
#&& chmod 700 get_helm.sh \
#&& ./get_helm.sh

# Install Azure CLI - ID09262019
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

# Install kubectl (latest)
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl \
&& chmod +x ./kubectl \
&& mv ./kubectl /usr/local/bin/kubectl

# Install Terraform
RUN wget --quiet https://releases.hashicorp.com/terraform/1.6.6/terraform_1.6.6_linux_amd64.zip \
  && unzip terraform_1.6.6_linux_amd64.zip \
  && mv terraform /usr/bin \
  && rm terraform_1.6.6_linux_amd64.zip

# Install Python3
#RUN apt-get install -y python3.6 \
#    && ln -s /usr/bin/python3.6 /usr/bin/python3
#RUN python3 -V


WORKDIR /azp/

COPY ./start.sh ./
RUN chmod +x ./start.sh

# Create agent user and set up home directory
RUN useradd -m -d /home/agent agent
RUN chown -R agent:agent /azp /home/agent

USER agent
# Another option is to run the agent as root.
# ENV AGENT_ALLOW_RUNASROOT="true"

ENTRYPOINT [ "./start.sh" ]