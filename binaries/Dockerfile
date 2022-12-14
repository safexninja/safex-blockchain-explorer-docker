FROM debian:buster

ENV VERSION=7.0.2

RUN apt-get update -y 
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install tzdata

RUN apt-get install -y \
    sudo \
    build-essential \ 
    cmake \
    make \
    libboost-all-dev \
    miniupnpc \
    graphviz \
    doxygen \
    pkg-config \
    libcurl4-openssl-dev \
    libgtest-dev \
    libreadline-dev \
    libsodium-dev \
    libzmq3-dev \
    libpcsclite-dev \
    libunwind8-dev \
    libssl-dev \ 
    libunbound-dev \ 
    libminiupnpc-dev \
    liblzma-dev \ 
    libldns-dev \
    libexpat1-dev \
    libprotobuf-dev \
    git-all \
    nano

ARG USER=docker
ENV HOME /home/$USER

RUN adduser --disabled-password --gecos '' $USER
RUN adduser $USER sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER $USER
WORKDIR $HOME

# Build safex core
RUN git clone --recursive https://github.com/safex/safexcore.git
WORKDIR $HOME/safexcore
RUN git checkout tags/$VERSION -b $VERSION
RUN make -j 2
RUN ln -s $HOME/safexcore/build/release/bin $HOME/daemon
 
WORKDIR $HOME

# Build safex blockhain explorer
RUN git clone https://github.com/safex/safex-blockchain-explorer.git
WORKDIR $HOME/safex-blockchain-explorer
COPY fixes/explorer/templates/header.html $HOME/safex-blockchain-explorer/src/templates/header.html
RUN mkdir build
WORKDIR $HOME/safex-blockchain-explorer/build
RUN cmake ..
RUN make -j 2
RUN ln -s $HOME/safex-blockchain-explorer/build $HOME/explorer

LABEL author="Safex.Ninja"
LABEL core-version=$VERSION
LABEL description="Running Safex Blockchain Explorer"
LABEL info="See https://github.com/safex/safex-blockchain-explorer"

