#
# Build LTTng (master branches by default) on top of a 'latest' Ubuntu image
# along with a functional development environment.
#
# This does not build an image that is fit for production use; its
# intended audience is LTTng developers.
#
FROM ubuntu:latest

ARG lttng_branch=master
ARG urcu_branch=stable-0.10
ARG bt_branch=master

LABEL maintainer="jeremie.galarneau@gmail.com"

# tzdata, installed by asciidoc, will ask for a timezone during install
ENV DEBIAN_FRONTEND noninteractive

# Install build dependancies (to use vlttng)
RUN apt-get update && apt-get --yes install emacs-nox \
                          git \
                          automake \
                          python3-pip \
                          bison \
                          flex \
                          autoconf \
                          libtool \
                          build-essential \
                          libxml2-dev \
                          libpopt-dev \
                          asciidoc \
                          gdb \
                          libnuma-dev \
                          uuid-dev \
                          libelf-dev \
                          libdw-dev \
			  tmux

RUN pip3 install vlttng

# Running as 'root' will cause the lttng-sessiond to load
# kernel modules, which will fail in a container. Moreover,
# the test suite will attempt to run the kernel tracing tests
# when it is run as 'root' (and fail).
#
# The build and installation of lttng occurs in a virtual
# environment and thus doesn't need to be done as 'root'.
RUN useradd -ms /bin/bash dev
USER dev

RUN vlttng -v -p babeltrace-${bt_branch} \
                         -p urcu-${urcu_branch} \
			 -p lttng-ust-${lttng_branch} \
			 -p lttng-tools-${lttng_branch} \
			 ~/lttng -j$(nproc)
