FROM debian:9.5
 
ARG SSH_MASTER_USER
ARG SSH_MASTER_PASS
 
RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    nano \
    sudo \
    git \
    openssh-server
 
COPY ssh_config /etc/ssh/ssh_config
COPY sshd_config /etc/ssh/sshd_config
COPY user.sh /usr/local/bin/user.sh
RUN chmod +x /usr/local/bin/user.sh
RUN /usr/local/bin/user.sh
RUN git config --global http.sslVerify false
RUN git clone https://github.com/commaai/openpilot.git /data/openpilot
COPY entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh
# COPY ssh_key /home/root/.ssh/
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
 
CMD tail -f /dev/null