ARG BASE=ghcr.io/schmidtdse/tensorflow

# torch-cuda image uses:
# ARG BASE=ghcr.io/schmidtdse/cuda

# cpu-flavor
# ARG BASE=ghcr.io/schmidtdse/base

FROM $BASE
COPY environment.yml /tmp/environment.yml
RUN mamba env update --file /tmp/environment.yml
