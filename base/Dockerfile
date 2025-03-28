ARG BASE=quay.io/jupyter/minimal-notebook:ubuntu-24.04

# cuda image uses:
# ARG BASE=quay.io/jupyter/pytorch-notebook:cuda12-ubuntu-24.04
FROM $BASE

# Make code-server extensions etc persist to container, not hub
ENV XDG_DATA_HOME=/opt/share
ENV PATH=/opt/share/pixi/bin:$PATH

## Grant user sudoer privileges
USER root
RUN adduser "$NB_USER" sudo && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >>/etc/sudoers

USER ${NB_USER}
# code-server (VSCode)
RUN sudo curl -fsSL https://code-server.dev/install.sh | sh && rm -rf .cache 

# apt utilities, code-server setup
COPY install_utilities.sh /tmp/install_utilities.sh
RUN sudo bash /tmp/install_utilities.sh

## Create user-owned workspace
RUN mkdir /workspace && chown -R ${NB_USER}:users /workspace

# install pixi
RUN curl -fsSL https://pixi.sh/install.sh | PIXI_HOME=/opt/share/pixi bash

COPY vscode-extensions.txt vscode-extensions.txt
RUN xargs -n 1 code-server --install-extension < vscode-extensions.txt

COPY environment.yml environment.yml
RUN conda update --all --solver=classic -n base -c conda-forge conda && \
    conda env update --file environment.yml

