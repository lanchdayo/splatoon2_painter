FROM mcr.microsoft.com/vscode/devcontainers/typescript-node:0-14
ARG USER_UID=$USER_UID
ARG USER_GID=$USER_GID
ARG USERNAME=root

# [Optional] Update UID/GID if needed
ENV APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=1
RUN if [ "$USER_GID" != "1000" ] || [ "$USER_UID" != "1000" ]; then \
        groupmod --gid $USER_GID $USERNAME \
        && usermod --uid $USER_UID --gid $USER_GID $USERNAME \
        && chown -R $USER_UID:$USER_GID /home/$USERNAME; \
    fi

# install yarn
ENV APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=1
RUN npm config set user root
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update \
    && apt-get install -y yarn

# Install Python
RUN apt install -y python2-minimal \
  && curl https://bootstrap.pypa.io/2.7/get-pip.py -o get-pip.py \
  && python ./get-pip.py \
  && python -m pip install Pillow \
  && rm -rf get-pip.py

# Install Other libraries
RUN apt-get install -y gcc-avr avr-libc zlib1g-dev
