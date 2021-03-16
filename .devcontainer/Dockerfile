FROM ubuntu:focal

#Locale
ENV LANG C.UTF-8

ENV DEBIAN_FRONTEND=noninteractive 

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Install needed packages, setup user and clean up.
RUN  apt-get update \
	&& apt-get install -y sudo \
	# && apt-get install -y openjdk-8-jdk-headless --no-install-recommends \
	# && apt-get install -y python3 python3-distutils python3-apt --no-install-recommends \
	&& apt-get install -y ca-certificates curl git --no-install-recommends \
	&& curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y \
	# && curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
	# && python3 get-pip.py \
	# Clean Up
	# && rm get-pip.py \
	&& apt-get autoremove -y \
	&& apt-get clean -y \
	&& rm -rf /var/lib/apt/lists/* \
	# Create a non-root user to use if preferred - see https://aka.ms/vscode-remote/containers/non-root-user.
	# [Optional] Add sudo support for the non-root user
	&& groupadd --gid $USER_GID $USERNAME \
	&& useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
	&& echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
	&& chmod 0440 /etc/sudoers.d/$USERNAME

ENV PATH "$PATH:/.cargo/bin"