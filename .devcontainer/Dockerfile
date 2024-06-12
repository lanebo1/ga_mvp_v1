FROM mcr.microsoft.com/vscode/devcontainers/anaconda:3

RUN conda create -y --name py36 python=3.6
RUN conda config --add channels conda-forge && conda config --set channel_priority strict
COPY pystsup/requirements.txt /tmp/requirements.txt
RUN conda install -n py36 -y -v --file /tmp/requirements.txt
RUN conda uninstall -y -n py36 pyomo
RUN conda run -n py36 pip install pyomo pygmo==2.11.3

#SHELL ["conda", "run", "-n", "py36", "/bin/bash", "-c"]

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get -y install xfce4-session xfce4-panel xfce4-terminal xfce4-goodies thunar xterm x11-utils screen

RUN curl -L -O https://github.com/TurboVNC/turbovnc/releases/download/3.1.1/turbovnc_3.1.1_amd64.deb && \
    apt-get -y install ./turbovnc_3.1.1_amd64.deb && \
    rm turbovnc_3.1.1_amd64.deb

ENV NOVNC_VERSION=1.4.0
ENV WEBSOCKETIFY_VERSION=0.10.0
RUN mkdir -p /usr/local/novnc && \
    curl -sSL https://github.com/novnc/noVNC/archive/v${NOVNC_VERSION}.zip -o /tmp/novnc-install.zip && \
    unzip /tmp/novnc-install.zip -d /usr/local/novnc && \
    cp /usr/local/novnc/noVNC-${NOVNC_VERSION}/vnc.html /usr/local/novnc/noVNC-${NOVNC_VERSION}/index.html && \
    curl -sSL https://github.com/novnc/websockify/archive/v${WEBSOCKETIFY_VERSION}.zip -o /tmp/websockify-install.zip && \
    unzip /tmp/websockify-install.zip -d /usr/local/novnc && \
    ln -s /usr/local/novnc/websockify-${WEBSOCKETIFY_VERSION} /usr/local/novnc/noVNC-${NOVNC_VERSION}/utils/websockify && \
    rm -f /tmp/websockify-install.zip /tmp/novnc-install.zip && \
    sed -i -E 's/^python /python3 /' /usr/local/novnc/websockify-${WEBSOCKETIFY_VERSION}/run

COPY . /app
WORKDIR /app
ENTRYPOINT [ "/app/entrypoint.sh" ]
EXPOSE 5801

CMD python GUI_Application.py
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

