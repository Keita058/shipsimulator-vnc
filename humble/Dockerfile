FROM tiryoh/ros2-desktop-vnc:humble
# LABEL maintainer="Keita Tabuchi"

ENV DISTRO humble

ENV USER ubuntu
ENV WORKDIR shipsimulator_ws
RUN mkdir -p /home/${USER}/${WORKDIR}/src && cd /home/${USER}/${WORKDIR}/src
WORKDIR /home/${USER}/${WORKDIR}/src

# initial set for no cache
ARG CACHEBUST=1

# set shipsimulator packages
RUN git clone -b Guidance_module https://github.com/Keita058/shipsimulator.git


# python library for running shipsim
RUN curl http://repo.ros2.org/repos.key | sudo apt-key add -
RUN apt-get update -q && \
    apt-get upgrade -yq && \
    apt-get install -yq python3-dev python3-pip python3-venv && \
    rm -rf /var/lib/apt/lists/*
RUN pip install pandas

# build
WORKDIR /home/${USER}/${WORKDIR}/
RUN . /opt/ros/${DISTRO}/setup.sh && colcon build