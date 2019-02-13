FROM debian:9.5
 
ARG SSH_MASTER_USER
ARG SSH_MASTER_PASS
 
RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    nano \
    sudo \
    git \
    openssh-server \
    build-essential \
    clang \
    vim \
    screen \
    wget \
    bzip2 \
    curl
# RUN echo "deb http://download.opensuse.org/repositories/network:/messaging:/zeromq:/release-stable/Debian_9.0/ ./" >> /etc/apt/sources.list
# RUN wget https://download.opensuse.org/repositories/network:/messaging:/zeromq:/release-stable/Debian_9.0/Release.key -O- | sudo apt-key add
# RUN apt-get install libzmq3-dev
# RUN curl https://raw.githubusercontent.com/kennethreitz/pipenv/master/get-pipenv.py | python

COPY ssh_config /etc/ssh/ssh_config
COPY sshd_config /etc/ssh/sshd_config
COPY user.sh /usr/local/bin/user.sh
RUN chmod +x /usr/local/bin/user.sh
RUN /usr/local/bin/user.sh
RUN cp /bin/bash /usr/bin/bash
RUN git config --global http.sslVerify false
RUN git clone https://github.com/commaai/openpilot.git /data/openpilot
# RUN mv /data/openpilot/requirements_openpilot.txt /data/openpilot/requirements.txt
# RUN cd /data/openpilot; pipenv install subprocess32 setproctitle enum cython setuptools pycapnp numpy scipy matplotlib zmq
# RUN cd /data/openpilot; pipenv install
COPY entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh
# COPY ssh_key /home/root/.ssh/
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
 
CMD tail -f /dev/null