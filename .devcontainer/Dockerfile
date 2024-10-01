ARG DC_REGISTRY=docker.io

############################################################
# BASE
############################################################

FROM ${DC_REGISTRY}/rust:1.81-bookworm AS base

############################################################
# SYSTEM
############################################################

FROM base AS system

RUN rustup component add clippy

############################################################
# USER
############################################################

FROM system AS user

ARG DC_USER=dev
ARG DC_UID=1000
ARG DC_GID=1000

# Create a user who can run sudo without password.
RUN addgroup --gid ${DC_GID} ${DC_USER} \
    && adduser --disabled-password --gecos '' --uid ${DC_UID} --gid ${DC_UID} ${DC_USER} \
    && usermod --append --groups sudo ${DC_USER} \
    && echo "%${DC_USER} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER ${DC_USER}
