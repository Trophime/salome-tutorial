FROM trophime/salome:9.13.0-bookworm
LABEL maintainer Christophe Trophime <christophe.trophime@lncmi.cnrs.fr>

USER root

# Avoid warnings by switching to noninteractive
ENV DEBIAN_FRONTEND=noninteractive

# This Dockerfile adds a non-root user with sudo access. Use the "remoteUser"
# property in devcontainer.json to use it. On Linux, the container user's GID/UIDs
# will be updated to match your local UID/GID (when using the dockerFile property).
# See https://aka.ms/vscode-remote/containers/non-root-user for details.
ARG USERNAME=feelpp
ARG USER_UID=1000
ARG USER_GID=$USER_UID
ARG VGLUSERS_ID=1001

ARG SALOME_VERSION=9.12.0
ARG PLATFORM=DB12
ARG MESHGEMS_KEY=meshgems_key_2023.h
ARG MESHGEMS_VERSION="2.15-1"
ARG MGKeyGen_VERSION="0.0.2"


# Setup demo environment variables
ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US.UTF-8 \
    LC_ALL=C.UTF-8 \
    PATH=/opt/SALOME-${SALOME_VERSION}-${PLATFORM}:$PATH \
    XLIB_SKIP_ARGB_VISUALS=1


# Set correct timezone
RUN apt-get update \
    && apt-get -y install --no-install-recommends tzdata \
    && echo "Europe/Paris" | tee /etc/timezone \
    && dpkg-reconfigure --frontend noninteractive tzdata

# Configure apt and install packages
RUN apt-get update \
    && apt-get -y install --no-install-recommends apt-utils dialog 2>&1 \
    # \
    # Verify git, process tools, lsb-release (useful for CLI installs) installed\
    && apt-get -y install git git-lfs iproute2 procps lsb-release bash-completion tree coreutils \
    #\
    # Install C++ tools\
    && apt-get -y install build-essential \
    && apt-get -y install g++ cmake \
    #\
    # Install python tools\
    && apt-get -y install python3-minimal libpython3-dev swig \
    && apt-get -y install python-is-python3 python3-pip python3-jinja2 \
    && apt-get -y install python3-autopep8 black yapf3 python3-bandit flake8 pydocstyle pylint python3-pytest mypy \
    #\
    # hack to get rid of python 2.7 \
    # && apt-get -y remove python-pyflakes pyflakes \
    # && apt-get -y autoremove \
    #\# [Optional] Add sudo support for the non-root user
    && apt-get install -y sudo \
    #&& if [ "$(lsb_release -cs)" = "focal" ]; then echo "Set disable_coredump false" > /etc/sudo.conf; fi \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME\
    && chmod 0440 /etc/sudoers.d/$USERNAME \
    # add github ssh key
    && mkdir -p ~${USERNAME}/.ssh/ \
    && ssh-keyscan github.com >> ~${USERNAME}/.ssh/known_hosts \
    && chown -R ${USERNAME}.$USER_GID ~${USERNAME}/.ssh \
    # \
    && mkdir -p /opt/DISTENE/license

# Install pre-requisite packages 
RUN apt-get -y install python3-pint python3-yaml python3-psutil python3-memory-profiler \
    libboost-all-dev libcppunit-dev liblapack-dev libxml2-dev \
    swig doxygen libgraphviz-dev \
    qttools5-dev libqt5svg5-dev libqt5x11extras5-dev qtxmlpatterns5-dev-tools \
    python3-sip-dev pyqt5-dev pyqt5-dev-tools libfreeimage-dev libqwt-qt5-dev llvm-dev \
    libopenblas-pthread-dev libcminpack-dev libnlopt-dev libeigen3-dev python3-statsmodels \
    python3-rich \
    && apt-get -y install python3-rich python3-natsort \
    && apt-get -y install debian-keyring lsb-release

RUN groupadd -g ${VGLUSERS_ID} vglusers && \
    usermod -a -G vglusers feelpp



# # Clean up
# RUN apt-get autoremove -y \
#     && apt-get clean -y \
#     && rm -rf /var/lib/apt/lists/*

# Switch back to dialog for any ad-hoc use of apt-get
ENV DEBIAN_FRONTEND=dialog

