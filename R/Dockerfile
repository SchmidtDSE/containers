FROM ghcr.io/schmidtdse/base

# Install R, RStudio
USER root

RUN curl -s https://raw.githubusercontent.com/rocker-org/ml/refs/heads/master/install_r.sh | bash
RUN curl -s https://raw.githubusercontent.com/rocker-org/ml/refs/heads/master/install_rstudio.sh | bash

USER ${NB_USER}

# We either must modify the official /workdir/pixi.toml, or we can use pixi add
# We don't need to activate pixi env, just be in the correct workdir
RUN cd ${DOCKER_WORKDIR} && pixi add jupyter-rsession-proxy

