FROM ghcr.io/schmidtdse/base:latest

USER root

RUN apt-get update && apt-get install nodejs npm sudo -y

USER jovyan

RUN sudo npm install -g npm@latest
