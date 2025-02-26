ARG BASE=quay.io/jupyter/minimal-notebook:ubuntu-24.04

# cuda image uses:
# ARG BASE=quay.io/jupyter/pytorch-notebook:cuda12-ubuntu-24.04

FROM $BASE

# Make code-server extensions etc persist to container, not hub
ENV XDG_DATA_HOME=/opt/share

USER root
# code-server (VSCode)
RUN curl -fsSL https://code-server.dev/install.sh | sh && rm -rf .cache 

# apt utilities, code-server setup
COPY install_utilities.sh /tmp/install_utilities.sh
RUN bash /tmp/install_utilities.sh

## Grant user sudoer privileges
RUN adduser "$NB_USER" sudo && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >>/etc/sudoers

USER ${NB_USER}

# install pixi
RUN curl -fsSL https://pixi.sh/install.sh | PIXI_HOME=/opt/share/pixi bash

COPY vscode-extensions.txt vscode-extensions.txt
RUN xargs -n 1 code-server --install-extension < vscode-extensions.txt

COPY environment.yml environment.yml
RUN conda update --all --solver=classic -n base -c conda-forge conda && \
    conda env update --file environment.yml

