FROM nvidia/cuda:11.0-cudnn8-devel-ubuntu18.04
LABEL maintainer="Piotr Błaszyński <pblaszynski@zut.edu.pl>"

ENV LANG C.UTF-8
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update &&\
    apt-get install -y software-properties-common \
    build-essential \
    git \
    wget \
    vim \
    curl \
    zip \
    zlib1g-dev \
    unzip \
    pkg-config \
    libgl-dev \
    libblas-dev \
    liblapack-dev \
    python3-tk \
    python3-wheel \
    graphviz \
    libhdf5-dev \
    python3.8 \
    python3.8-dev \
    python3.8-distutils \
    swig \
    apt-transport-https \
    lsb-release \
    ca-certificates &&\
    # obtain latest of nodejs
    curl -sL https://deb.nodesource.com/setup_12.x | bash - &&\
    apt install -y nodejs &&\
    apt-get clean &&\
    ln -s /usr/bin/python3.8 /usr/local/bin/python &&\
    ln -s /usr/bin/python3.8 /usr/local/bin/python3 &&\
    curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py &&\
    python3 get-pip.py &&\
    rm get-pip.py &&\
    # best practice to keep the Docker image lean
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /src

# Install essential Python packages
RUN python3 -m pip --no-cache-dir install \
    blackcellmagic\
    pytest \
    pytest-cov \
    numpy \
    matplotlib \
    scipy \
    pandas \
    jupyter \
    scikit-learn \
    scikit-image \
    seaborn \
    graphviz \
    gpustat \
    h5py \
    gitpython \
    ptvsd \
    Pillow==6.1.0 \
    opencv-python
RUN python3 -m pip --no-cache-dir install \
    torch==1.7.0+cu110 \
    torchvision==0.8.1+cu110 \
    torchaudio===0.7.0 \
    -f https://download.pytorch.org/whl/torch_stable.html \
    'jupyterlab>=2' \
    xeus-python

RUN python3 -m pip --no-cache-dir install datajoint==0.12.7


# Add profiling library support
ENV LD_LIBRARY_PATH /usr/local/cuda/extras/CUPTI/lib64:${LD_LIBRARY_PATH}
