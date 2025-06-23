FROM ghcr.io/prefix-dev/pixi:noble AS build
LABEL "org.opencontainers.image.description"="A pixi-based Docker image for a robust GeoJupyter environment"

# Use bash as default shell instead of sh
ENV SHELL=/bin/bash
# Don't buffer Python stdout/stderr output
ENV PYTHONBUFFERED=1
# Don't prompt in apt commands
ENV DEBIAN_FRONTEND=noninteractive

# Set up JupyterLab user
ENV NB_USER=jovyan
ENV NB_UID=1000
ENV USER="${NB_USER}"
ENV HOME="/home/${NB_USER}"
RUN userdel ubuntu \
 && groupadd \
  --gid ${NB_UID} \
  ${NB_USER} \
 && useradd \
  --comment "Default Jupyter user" \
  --create-home \
  --no-log-init \
  --uid ${NB_UID} \
  --gid ${NB_UID} \
  --shell ${SHELL} \
  ${NB_USER}

ENV DOCKER_WORKDIR=/workdir
WORKDIR ${DOCKER_WORKDIR}
RUN chown ${NB_UID}:${NB_UID} ${DOCKER_WORKDIR}

# this env var is recognized by jupyter-vscode-proxy:
ENV CODE_EXTENSIONSDIR=/opt/share/code-server
# put quarto on the path too
ENV PATH=$PATH:/usr/lib/rstudio-server/bin/quarto/bin

USER root
# code-server (VSCode)
RUN apt-get update -q && apt-get -y install curl && apt-get clean && rm -rf /var/lib/apt/lists/*
RUN mkdir -p ${CODE_EXTENSIONSDIR} && chown -R ${NB_USER}:users ${CODE_EXTENSIONSDIR}
RUN curl -fsSL https://code-server.dev/install.sh | sh && rm -rf /home/${NB_USER}/.cache 

# Install R, RStudio
RUN curl -s https://raw.githubusercontent.com/rocker-org/ml/refs/heads/master/install_r.sh | bash
RUN curl -s https://raw.githubusercontent.com/rocker-org/ml/refs/heads/master/install_rstudio.sh | bash

# Build the environment
USER ${NB_USER}

COPY vscode-extensions.txt /tmp/vscode-extensions.txt
RUN xargs -n 1 code-server --extensions-dir ${CODE_EXTENSIONSDIR} --install-extension < /tmp/vscode-extensions.txt

COPY pixi.toml .
RUN pixi install \
 && rm -rf ~/.cache/rattler

# Set up shell activation script
 RUN pixi shell-hook -s bash > ./shell-hook
USER root
ENV ENTRYPOINT_SCRIPT="/entrypoint.sh"
RUN echo "#!/bin/bash" > ${ENTRYPOINT_SCRIPT}
 RUN cat ${PWD}/shell-hook >> ${ENTRYPOINT_SCRIPT}
RUN echo 'exec "$@"' >> ${ENTRYPOINT_SCRIPT}
RUN chmod +x ${ENTRYPOINT_SCRIPT}

USER ${NB_USER}
WORKDIR "/home/${NB_USER}"
EXPOSE 8888
ENTRYPOINT ["/entrypoint.sh"]
CMD ["jupyter", "lab", "--no-browser", "--ip=0.0.0.0"]
