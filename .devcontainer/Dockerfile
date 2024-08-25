ARG IMAGE_VARIANT=ubuntu-22.04
ARG PYTHON_VERSION=3.11
ARG USER=vscode

FROM mcr.microsoft.com/devcontainers/base:${IMAGE_VARIANT}

ARG DEBIAN_FRONTEND=noninteractive
ARG USER=vscode
RUN apt update \
    && apt install -y --no-install-recommends curl wget git sudo build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev \
    && apt install -y --no-install-recommends python3-venv \
    && apt autoremove -y \
    && rm -rf /var/lib/apt/lists/* \
    && usermod -s /usr/bin/zsh ${USER}

USER ${USER}
ARG HOME="/home/${USER}"
WORKDIR ${HOME}

ARG PYTHON_VERSION=${PYTHON_VERSION}
ARG PDM_PATH="${HOME}/.local/bin"
ENV PATH="${PYENV_PATH}:${PDM_PATH}:$PATH"

ARG ZSH_CUSTOM=${HOME}/.oh-my-zsh/custom
RUN curl -sSL https://pdm-project.org/install-pdm.py | python3 - \
    && mkdir ${ZSH_CUSTOM}/plugins/pdm \
    && pdm completion zsh > ${ZSH_CUSTOM}/plugins/pdm/_pdm \
    && sed -i "s|^plugins=(|&pdm |" ${HOME}/.zshrc