FROM ubuntu:16.04
MAINTAINER James Hunt <jhunt@starkandwayne.com>

#===============
# Configuration
#===============
ENV PACKAGES "ruby openssl wget git unzip curl ca-certificates tmux tree vim netcat-openbsd less"

ENV BOSH_INIT_VERSION 0.0.100
ENV BOSH_INIT_URL https://s3.amazonaws.com/bosh-init-artifacts/bosh-init-${BOSH_INIT_VERSION}-linux-amd64
ENV BOSH_CLI_V2_VERSION 3.0.1
ENV VAULT_CLI_VERSION 0.10.0
ENV FLY_VERSION 3.8.0
ENV SAFE_VERSION 0.8.1
ENV SPRUCE_VERSION 1.17.0
ENV JQ_VERSION 1.5
ENV OM_VERSION 0.35.0
ENV TERRAFORM_VERSION 0.10.7

#===============
# Initial Setup
#===============
RUN apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends ${PACKAGES} \
  && rm -rf /var/lib/apt/lists/*

#===========
# bosh-init
#===========
RUN wget -q -O /usr/local/bin/bosh-init --no-check-certificate ${BOSH_INIT_URL} \
  && chmod +x /usr/local/bin/bosh-init

#====
# jq
#====
RUN wget -q -O /usr/local/bin/jq --no-check-certificate https://github.com/stedolan/jq/releases/download/jq-${JQ_VERSION}/jq-linux64 \
  && chmod +x /usr/local/bin/jq

#========
# spruce
#========
RUN wget -q -O /usr/local/bin/spruce --no-check-certificate http://github.com/geofffranks/spruce/releases/download/v${SPRUCE_VERSION}/spruce-linux-amd64 \
  && chmod +x /usr/local/bin/spruce

#=============
# bosh-cli v2
#=============
RUN wget -q -O /usr/local/bin/bosh-cli --no-check-certificate https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-${BOSH_CLI_V2_VERSION}-linux-amd64 \
  && chmod +x /usr/local/bin/bosh-cli

#=============================
# Vault
# https://www.vaultproject.io
#=============================
RUN wget -q --no-check-certificate https://releases.hashicorp.com/vault/${VAULT_CLI_VERSION}/vault_${VAULT_CLI_VERSION}_linux_amd64.zip \
  && unzip vault_${VAULT_CLI_VERSION}_linux_amd64.zip \
  && mv vault /usr/local/bin \
  && rm vault_${VAULT_CLI_VERSION}_linux_amd64.zip

#=======================================
# Safe
# https://github.com/starkandwayne/safe
#=======================================
RUN wget -q --no-check-certificate http://github.com/starkandwayne/safe/releases/download/v${SAFE_VERSION}/safe-linux-amd64 \
  && mv safe-linux-amd64 /usr/local/bin/safe \
  && chmod 777 /usr/local/bin/safe

#========
# CF CLI
#========
RUN wget -q --no-check-certificate -O stable.tgz "https://cli.run.pivotal.io/stable?release=linux64-binary&source=github" \
  && tar xf stable.tgz cf \
  && mv cf /usr/local/bin \
  && rm stable.tgz

#=====
# fly
#=====
RUN wget -q -O /usr/local/bin/fly --no-check-certificate https://github.com/concourse/concourse/releases/download/v${FLY_VERSION}/fly_linux_amd64 \
  && chmod +x /usr/local/bin/fly

#=============================
# Install Om
#==============================
RUN wget -q -O /usr/local/bin/om --no-check-certificate https://github.com/pivotal-cf/om/releases/download/${OM_VERSION}/om-linux \
  && chmod +x /usr/local/bin/om

#============================
# terraform
# https://www.terraform.io
#===========================
RUN wget -q --no-check-certificate https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
  && unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
  && mv terraform /usr/local/bin \
  && chmod +x /usr/local/bin/terraform \
  && rm terraform_${TERRAFORM_VERSION}_linux_amd64.zip

CMD /bin/bash
