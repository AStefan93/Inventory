# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.245.2/containers/ubuntu/.devcontainer/base.Dockerfile

FROM gitpod/workspace-full-vnc

# Prerequisites
RUN apt update && apt install -y curl git unzip xz-utils zip libglu1-mesa openjdk-8-jdk wget clang cmake ninja-build pkg-config libgtk-3-dev liblzma-dev

# Install latest git version
RUN apt-get install software-properties-common -y && apt-add-repository ppa:git-core/ppa && apt-get update && apt-get install git -y

# Install Android Studio
RUN apt-get install software-properties-common -y && apt-add-repository ppa:maarten-fonville/android-studio && apt-get update && apt-get install android-studio -y

ARG USERNAME=vscode
USER $USERNAME
WORKDIR /home/$USERNAME
ENV DISPLAY=:0

# Prepare Android directories and system variables
RUN mkdir -p Android/sdk
ENV ANDROID_SDK_ROOT /home/$USERNAME/Android/sdk
RUN mkdir -p .android && touch .android/repositories.cfg

# Set up Android SDK
RUN wget -O sdk-tools.zip https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip
RUN unzip sdk-tools.zip && rm sdk-tools.zip
RUN mv tools Android/sdk/tools
RUN cd Android/sdk/tools/bin && yes | ./sdkmanager --licenses
RUN cd Android/sdk/tools/bin && ./sdkmanager "cmdline-tools;latest" "build-tools;29.0.2" "patcher;v4" "platform-tools" "platforms;android-29" "sources;android-29"
ENV PATH "$PATH:/home/$USERNAME/Android/sdk/"
ENV PATH "$PATH:/home/$USERNAME/Android/sdk/platform-tools"
ENV PATH "$PATH:/home/$USERNAME/Android/sdk/cmdline-tools/latest/bin"
ENV PATH "$PATH:/home/$USERNAME/Android/sdk/cmdline-tools/latest/bin"

# Download Flutter SDK
RUN git clone https://github.com/flutter/flutter.git
ENV PATH "$PATH:/home/$USERNAME/flutter/bin"

# Install Chrome for Web Development
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && sudo apt-get install -y ./google-chrome-stable_current_amd64.deb
RUN rm google-chrome-stable_current_amd64.deb

# Run basic check to download Dark SDK
RUN flutter doctor
