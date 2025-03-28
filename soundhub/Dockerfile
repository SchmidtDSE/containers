# Example use: specify a FROM in a Dockerfile at the top (root) level of your repo
#FROM quay.io/jupyter/pytorch-notebook:cuda12-ubuntu-24.04
FROM ghcr.io/schmidtdse/cuda
# let's do this with pixi instead?
COPY environment.yml /tmp/environment.yml
RUN conda update --all --solver=classic -n base -c conda-forge conda && conda env update --file /tmp/environment.yml

