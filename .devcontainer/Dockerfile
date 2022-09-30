FROM gitpod/workspace-full-vnc

# Prerequisites
RUN sudo apt-get update && sudo apt-get install -y curl git unzip xz-utils zip libglu1-mesa openjdk-8-jdk wget clang cmake ninja-build pkg-config libgtk-3-dev liblzma-dev

# Install latest git version
RUN sudo apt-get install software-properties-common -y && sudo apt-add-repository ppa:git-core/ppa && sudo apt-get update && sudo apt-get install git -y

# Install Android Studio
RUN sudo apt-get install software-properties-common -y && sudo apt-add-repository ppa:maarten-fonville/android-studio && sudo apt-get update && sudo apt-get install android-studio -y

ARG USERNAME=gitpod
USER $USERNAME
WORKDIR /home/$USERNAME

# Prepare Android directories and system variables
RUN sudo mkdir -p Android/sdk
ENV ANDROID_SDK_ROOT /home/$USERNAME/Android/sdk
RUN sudo mkdir -p .android && sudo touch .android/repositories.cfg

# Set up Android SDK
RUN sudo wget -O sdk-tools.zip https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip
RUN sudo unzip sdk-tools.zip && sudo rm sdk-tools.zip
RUN sudo mv tools Android/sdk/tools
RUN cd Android/sdk/tools/bin && yes | sudo ./sdkmanager --licenses
RUN cd Android/sdk/tools/bin && sudo ./sdkmanager "cmdline-tools;latest" "build-tools;29.0.2" "patcher;v4" "platform-tools" "platforms;android-29" "sources;android-29"
ENV PATH "$PATH:/home/$USERNAME/Android/sdk/"
ENV PATH "$PATH:/home/$USERNAME/Android/sdk/platform-tools"
ENV PATH "$PATH:/home/$USERNAME/Android/sdk/cmdline-tools/latest/bin"
ENV PATH "$PATH:/home/$USERNAME/Android/sdk/cmdline-tools/latest/bin"

# Download Flutter SDK
RUN git clone https://github.com/flutter/flutter.git
ENV PATH "$PATH:/home/$USERNAME/flutter/bin"

# Install Chrome for Web Development
RUN sudo wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && sudo apt-get install -y ./google-chrome-stable_current_amd64.deb
RUN sudo rm google-chrome-stable_current_amd64.deb

# Run basic check to download Dark SDK
RUN flutter doctor
