# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.245.2/containers/alpine/.devcontainer/base.Dockerfile

# [Choice] Alpine version: 3.16, 3.15, 3.14, 3.13
ARG VARIANT="3.16"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-alpine-${VARIANT}

# Install additional packages
RUN apk update \
  && apk add --no-cache \
  zip \
  # tools for building iso images
  alpine-sdk build-base apk-tools alpine-conf busybox fakeroot syslinux xorriso squashfs-tools sudo \
  # tools for efi
  mtools dosfstools grub-efi 

WORKDIR /home/vscode

# Copy the aports repo into the container
ADD https://gitlab.alpinelinux.org/alpine/aports/-/archive/master/aports-master.zip ./

RUN unzip aports-master \
  && mv aports-master aports \
  && rm aports-master.zip

WORKDIR /

# Create signing keys
RUN abuild-keygen \
  # Set PACKAGER_PRIVKEY=<generated key> in abuild.conf
  -a \ 
  # Install public key into /etc/apk/keys using sudo
  -i \
  # Non-interactive. Use defaults
  -n 
