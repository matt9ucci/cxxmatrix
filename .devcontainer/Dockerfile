ARG UBUNTU_VERSION=latest
FROM ubuntu:$UBUNTU_VERSION

ARG EMSDK_VERSION=latest

RUN apt-get update \
	&& DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends \
		bash-completion \
		build-essential \
		ca-certificates \
		curl \
		gdb \
		git \
		python3 \
		xz-utils \
	&& rm -rf /var/lib/apt/lists/*

WORKDIR /root

# Install emsdk
# https://emscripten.org/docs/getting_started/downloads.html
RUN git clone --depth 1 https://github.com/emscripten-core/emsdk.git \
	&& ./emsdk/emsdk install $EMSDK_VERSION \
	&& ./emsdk/emsdk activate $EMSDK_VERSION \
	&& echo "source $(realpath ./emsdk/emsdk_env.sh) > /dev/null 2>&1" >> ~/.bashrc

RUN echo "\
alias c='code'\n\
alias g='git'\n\
\n\
alias cd..='cd ..'\n\
alias sl='cd'\n\
alias sl..='cd ..'\n\
" > ~/.bash_aliases \
	&& sed -i -E 's/\s*#\s*(force_color_prompt=yes)/\1/1' ~/.bashrc \
	&& echo "\n\
source /etc/profile.d/bash_completion.sh\n\
" >> ~/.bashrc
