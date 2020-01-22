FROM btlk/ubuntu-20.04

LABEL maintainer="Alexander Serikov <ivanmitrafanych@gmail.com>"

# Set development stuff
RUN apt-add-repository -y ppa:ubuntu-toolchain-r/test \
 && apt-get update \
 && apt-get install -y --no-install-recommends \
    gcc-9 \
    g++-9 \
    gdb \
    libgtest-dev \
    google-mock \
    linux-tools-generic \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 && ln -sf /usr/bin/g++-9 /usr/bin/g++ \
 && ln -sf /usr/bin/gcc-9 /usr/bin/gcc

ENV CC gcc
ENV CXX g++

# Set vscode
ARG VSCODE_VERSION=1.41.1

ENV SHELL /bin/bash
ENV DOWNLOAD_URL https://vscode-update.azurewebsites.net/$VSCODE_VERSION/linux-deb-x64/stable

RUN wget -q "$DOWNLOAD_URL" -O code.deb

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    firefox \
    libasound2 \
    libgtk-3-0 \
    libxtst6 \
    libx11-xcb-dev \
    ./code.deb \
 && apt-get clean \
 && rm ./code.deb \
 && rm -rf /var/lib/apt/lists/*

ADD keep_running.sh /postprocess.d/

CMD ["code"]
