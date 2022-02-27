FROM ubuntu:20.04

# You can replace that with yourself
ARG UNAME=build
ARG UID=1000
ARG GID=1000

SHELL [ "/bin/bash", "-o", "pipefail", "-c" ]

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
      apt \
      build-essential \
      git \
      python3 \
      python3-pip \
      python3.8-venv \
#      shellcheck \
      && apt-get clean && rm -rf /var/lib/apt/lists/*

# Getting the environment ready
ENV HOME /home/${UNAME}
RUN groupadd -g ${GID} -o ${UNAME}
RUN useradd -l -rm -d ${HOME} -u ${UID} -g ${GID} -s /bin/bash ${UNAME}
USER ${UNAME}

WORKDIR ${HOME}
RUN mkdir -p ${HOME}/build

# Installing pre-commit
ENV VIRTUAL_ENV=${HOME}/.local
RUN python3 -m venv ${VIRTUAL_ENV}
ENV PATH="${VIRTUAL_ENV}/bin:${PATH}"
#RUN pip3 --no-cache-dir install pre-commit

# Default configuration
#COPY --chown=${UNAME}:${UNAME} .pre-commit-config.yaml /config/
WORKDIR ${HOME}/build/
