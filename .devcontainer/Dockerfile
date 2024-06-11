FROM mcr.microsoft.com/vscode/devcontainers/anaconda:3

RUN conda config --add channels conda-forge && conda config --set channel_priority strict && conda install pygmo
COPY pystsup/requirements.txt /tmp/requirements.txt
RUN conda install --file /tmp/requirements.txt

# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends \
#     python3-pip \
#     libboost-all-dev \
#     cmake \
#     && apt-get clean && rm -rf /var/lib/apt/lists/*

# RUN git clone https://github.com/esa/pagmo.git \
#     && cd pagmo \
#     && mkdir build \
#     && cd build \
#     && cmake .. \
#     && make -j4 \
#     && make install

# COPY requirements.txt /tmp/requirements.txt
# RUN pip3 install --no-cache-dir -r /tmp/requirements.txt

