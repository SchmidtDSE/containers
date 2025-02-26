ARG BASE=ghcr.io/schmidtdse/base 
FROM $BASE

COPY vscode-extensions.txt vscode-extensions.txt
RUN xargs -n 1 code-server --install-extension < vscode-extensions.txt

COPY pixi.lock /workspace/pixi.lock
COPY pixi.toml /workspace/pixi.toml

WORKDIR /workspace
RUN pixi install


