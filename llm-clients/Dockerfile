FROM ghcr.io/schmidtdse/base:latest

ENV NVM_DIR=/opt/nvm
USER root
RUN mkdir /opt/nvm && chown -R 1000:1000 /opt/nvm

RUN apt-get update && apt-get -y install libatomic1 python3-venv python-is-python3 build-essential 

USER jovyan
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash \
    && . "$NVM_DIR/nvm.sh" \
    && nvm install node \
    && nvm alias default node \
    && nvm use default

# Add Node.js and npm to the PATH
ENV NVM_VERSION=v25.1.0
ENV NODE_PATH=$NVM_DIR/versions/node/$NVM_VERSION/lib/node_modules
ENV PATH=$NVM_DIR/versions/node/$NVM_VERSION/bin:$PATH


SHELL ["/bin/bash", "-c"]
RUN npm install -g @openai/codex
RUN npm install -g @github/copilot
RUN npm install -g @anthropic-ai/claude-code
RUN npm install -g cline



