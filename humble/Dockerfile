FROM tiryoh/ros2-desktop-vnc:humble
# LABEL maintainer="Keita Tabuchi<tabuchi-keita-wm@ynu.jp>"

ENV DISTRO humble

ENV USER ubuntu
#ENV WORKDIR shipsimulator_ws
#RUN mkdir -p /home/${USER}/${WORKDIR}/src && cd /home/${USER}/${WORKDIR}/src
#WORKDIR /home/${USER}/${WORKDIR}/src
RUN mkdir -p /home/${USER} && cd /home/${USER}
WORKDIR /home/${USER}

# initial set for no cache
ARG CACHEBUST=1

# set shipsimulator packages
RUN git clone -b Guidance_module --depth 1 https://github.com/Keita058/shipsimulator.git

# python library for running shipsim
RUN curl http://repo.ros2.org/repos.key | sudo apt-key add -
RUN apt-get update -q && \
    apt-get upgrade -yq && \
    apt-get install -yq python3-dev python3-pip python3-venv && \
    rm -rf /var/lib/apt/lists/*
RUN pip install pandas

## Install chrome browser
#RUN apt-get update && apt-get install -y wget gnupg
#RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
#RUN echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list
#RUN apt-get update && apt-get install -y google-chrome-stable

# Install Unity Hub
RUN wget -qO - https://hub.unity3d.com/linux/keys/public | gpg --dearmor | sudo tee /usr/share/keyrings/Unity_Technologies_ApS.gpg > /dev/null
RUN sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/Unity_Technologies_ApS.gpg] https://hub.unity3d.com/linux/repos/deb stable main" > /etc/apt/sources.list.d/unityhub.list'
RUN apt-get update && apt-get install -y unityhub
RUN ln -s /opt/UnityHub/unityhub /home/${USER}/Desktop/unityhub

WORKDIR /home/${USER}/shipsimulator
RUN . /opt/ros/${DISTRO}/setup.sh && colcon build