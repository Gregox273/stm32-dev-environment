# v1.0
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
    python3-pip \
    ruby=1:2.7+1 \
    unzip \
    valgrind  \
    wget \
    && apt-get autoremove -y \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
# Install ceedling and cpplint
    && gem install ceedling:'<= 0.31.0' \
    && pip3 install 'cpplint==1.5.5' 

# Install gcc-arm-none-eabi
WORKDIR /home/dev
RUN wget https://developer.arm.com/-/media/Files/downloads/gnu-rm/10-2020q4/gcc-arm-none-eabi-10-2020-q4-major-x86_64-linux.tar.bz2 \
    && tar xvf gcc-arm-none-eabi-10-2020-q4-major-x86_64-linux.tar.bz2 \
    && rm gcc-arm-none-eabi-10-2020-q4-major-x86_64-linux.tar.bz2

# Set up the compiler path
ENV PATH $PATH:/home/dev/gcc-arm-none-eabi-10-2020-q4-major/bin

WORKDIR /app