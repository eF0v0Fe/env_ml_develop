FROM nvidia/cuda:11.2.2-cudnn8-devel-ubuntu20.04

#Basic Setting Library
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
    && apt-get install --yes --no-install-recommends \
    sudo \
    git \
    tig \
    cmake \
    pkg-config \
    unzip \
    wget \
    vim \
    build-essential \
    libssl-dev \
    libbz2-dev \
    libreadline-dev \
    libsqlite3-dev \
    libffi-dev \
    curl \
    libsm6 \
    libgtk2.0-dev \
    less \
    pv \
    zlib1g-dev \
    llvm \
    libncurses5-dev \
    libncursesw5-dev \
    xz-utils \
    tk-dev \
    liblzma-dev \
    libgl1-mesa-dev \
    ffmpeg \
    ninja-build \
    libglib2.0-0 \
    libxext6 \
    && rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*

# Sudo User
ARG USERNAME
RUN useradd ${USERNAME} -G sudo -s /bin/bash -m && \
    echo ${USERNAME} 'ALL=(ALL) NOPASSWD:ALL'>>/etc/sudoers && \
    chown ${USERNAME}:${USERNAME} /home/${USERNAME}
    
USER ${USERNAME}
WORKDIR /home/${USERNAME}
ENV HOME /home/${USERNAME}

# Install pyenv
ENV PYTHON_VERSION 3.10.4
ENV PYENV_ROOT /home/${USERNAME}/.pyenv
ENV PATH $PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH
RUN curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash
RUN pyenv install ${PYTHON_VERSION} && pyenv global ${PYTHON_VERSION}

# Install pip
RUN pip install -U pip setuptools
RUN pip install --upgrade pip

RUN sudo apt clean && sudo apt autoremove