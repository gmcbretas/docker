FROM centos:5
LABEL maintainer="Shaun Jackman <sjackman@gmail.com>"
LABEL name="Linuxbrew/centos5"

ADD https://gist.github.com/sjackman/132b65c33b62a89c45671e9c605025bc/raw/CentOS-Base.repo /etc/yum.repos.d/
ADD	https://gist.github.com/sjackman/132b65c33b62a89c45671e9c605025bc/raw/libselinux.repo /etc/yum.repos.d/
RUN	yum install -y curl gcc gcc44 gcc44-c++ make sudo which
RUN	yum clean all

RUN localedef -i en_US -f UTF-8 en_US.UTF-8 \
	&& useradd -m -s /bin/bash linuxbrew \
	&& echo 'linuxbrew ALL=(ALL) NOPASSWD:ALL' >>/etc/sudoers

USER linuxbrew
WORKDIR /home/linuxbrew

ENV PATH=/home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/sbin:$PATH \
	SHELL=/bin/bash \
	USER=linuxbrew

# Install Linuxbrew.
# Create symlinks for GCC 4.4.
# Install a recent version of file that supports --print0.
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/Linuxbrew/install/master/install.sh)"
RUN	ln -s /usr/bin/gcc44 ~/.linuxbrew/bin/gcc-4.4
RUN	ln -s /usr/bin/g++44 ~/.linuxbrew/bin/g++-4.4
RUN	HOMEBREW_BUILD_FROM_SOURCE=1 HOMEBREW_NO_AUTO_UPDATE=1 brew install file-formula
RUN	brew config
