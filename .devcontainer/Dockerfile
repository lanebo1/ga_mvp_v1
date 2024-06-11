FROM mcr.microsoft.com/vscode/devcontainers/anaconda:3

RUN conda create -y --name py36 python=3.6
RUN conda config --add channels conda-forge && conda config --set channel_priority strict
COPY pystsup/requirements.txt /tmp/requirements.txt
RUN conda install -n py36 -y -v --file /tmp/requirements.txt

#SHELL ["conda", "run", "-n", "py36", "/bin/bash", "-c"]

COPY . /app
WORKDIR /app
CMD [ "source activate py36; python GUI_Application.py" ]
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

