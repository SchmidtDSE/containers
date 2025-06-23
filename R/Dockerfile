FROM ghcr.io/schmidtdse/base

# Install R, RStudio
USER root

RUN curl -s https://raw.githubusercontent.com/rocker-org/ml/refs/heads/master/install_r.sh | bash
RUN curl -s https://raw.githubusercontent.com/rocker-org/ml/refs/heads/master/install_rstudio.sh | bash

USER ${NB_USER}

