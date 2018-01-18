FROM ubuntu:16.04

RUN apt-get update

# gmp dependencies
RUN apt-get install -y \
        build-essential \
        m4 \
        wget
# gmp download or just: apt intall libgmp3-dev
ENV GMP_VERSION 6.1.2
WORKDIR /root
RUN wget https://gmplib.org/download/gmp/gmp-${GMP_VERSION}.tar.xz && \
    mkdir gmp && \
    tar -xvf gmp-${GMP_VERSION}.tar.xz --strip=1 -C gmp/ && \
    rm gmp-${GMP_VERSION}.tar.xz
# gmp install
RUN cd /root/gmp && \
    ./configure && \
    make -j$(nproc) && \
    make install


# pbc dependencies
RUN apt-get install -y \
        bison \
        flex
# pbc download
ENV PBC_VERSION 0.5.14
WORKDIR /root
RUN wget https://crypto.stanford.edu/pbc/files/pbc-${PBC_VERSION}.tar.gz && \
    mkdir pbc && \
    tar -xvzf pbc-${PBC_VERSION}.tar.gz --strip=1 -C pbc/ && \
    rm pbc-${PBC_VERSION}.tar.gz
# pbc install
RUN cd /root/pbc && \
    ./configure && \
    make -j$(nproc) && \
    make install


# charm dependencies
RUN apt-get install -y \
        git \
        libgmp3-dev \
        libssl-dev \
        python3-dev \
        python3-setuptools
# charm download
RUN git clone https://github.com/JHUISI/charm.git
# charm install
RUN cd /root/charm && \
    ./configure.sh && \
    make -j$(nproc) && \
    make install


# abe download
RUN git clone https://github.com/sagrawal87/ABE.git
# abe fix
RUN cd /root/ABE && \
    2to3-3.5 -w *.py && \
    sed -i -e 's/debug = False/debug = True/g' main.py
