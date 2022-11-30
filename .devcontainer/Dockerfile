FROM qmcgaw/latexdevcontainer:latest-full
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN apt-get update -y
RUN apt-get install -y python3 python3-pip
RUN pip3 install pygments pandas
RUN apt-get -y install sudo

RUN tlmgr update --self && \
    tlmgr install enumitem lastpage pythontex

RUN groupadd --gid $USER_GID $USERNAME && \
    useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME && \
    echo "$USERNAME:$USERNAME" | chpasswd && \
    usermod -aG sudo $USERNAME && \
    ln -s /usr/bin/python3.9 /usr/bin/python

USER $USERNAME