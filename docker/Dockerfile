# v1.1
FROM ubuntu:20.04

LABEL maintainer="greg.brooks@gregox.com"

WORKDIR /app

ARG DEBIAN_FRONTEND=noninteractive

# apt-get install packages
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    build-essential \
    bzip2 \
    cmake=3.16.3-1ubuntu1 \
    git \
    libncurses-dev \
    python3-pip \
    ruby=1:2.7+1 \
    unzip \
    valgrind  \
    wget \
    && apt-get autoremove -y \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
# Install ceedling and cpplint
    && gem install ceedling:'<= 0.31.0' \
    && pip3 install 'cpplint==1.5.5' \
# Symbolic links to make gdb work
    && ln -s /usr/lib/x86_64-linux-gnu/libncurses.so.6 /usr/lib/x86_64-linux-gnu/libncurses.so.5 \
    && ln -s /usr/lib/x86_64-linux-gnu/libtinfo.so.6 /usr/lib/x86_64-linux-gnu/libtinfo.so.5

# Install gcc-arm-none-eabi
WORKDIR /home/dev
RUN wget https://developer.arm.com/-/media/Files/downloads/gnu-rm/10-2020q4/gcc-arm-none-eabi-10-2020-q4-major-x86_64-linux.tar.bz2 \
    && tar xvf gcc-arm-none-eabi-10-2020-q4-major-x86_64-linux.tar.bz2 \
    && rm gcc-arm-none-eabi-10-2020-q4-major-x86_64-linux.tar.bz2

# Set up the compiler path
ENV PATH $PATH:/home/dev/gcc-arm-none-eabi-10-2020-q4-major/bin

WORKDIR /app