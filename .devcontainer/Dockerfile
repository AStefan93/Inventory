# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.245.2/containers/ubuntu/.devcontainer/base.Dockerfile

ARG VARIANT="ubuntu-22.04"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

# Java
RUN apt-get update && apt-get -y install build-essential openjdk-11-jdk

# Android SDK
RUN apt-get install software-properties-common -y && apt-add-repository ppa:maarten-fonville/android-studio && apt-get update && apt-get install android-studio -y

# Install latest git version
RUN apt-get install software-properties-common -y && apt-add-repository ppa:git-core/ppa && apt-get update && apt-get install git -y

# Flutter
RUN git clone https://github.com/flutter/flutter.git
ENV PATH "$PATH:~/flutter/bin"

# RUN flutter doctor