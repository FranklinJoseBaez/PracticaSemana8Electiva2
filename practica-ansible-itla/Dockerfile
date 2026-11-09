
FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    openssh-server \
    sudo \
    python3 \
    && useradd -m -s /bin/bash ansible \
    && echo "ansible:ansible" | chpasswd \
    && echo "ansible ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/ansible \
    && chmod 0440 /etc/sudoers.d/ansible \
    && mkdir -p /run/sshd \
    && echo "PasswordAuthentication yes" > /etc/ssh/sshd_config.d/ansible.conf \
    && rm -f /etc/ssh/ssh_host_*_key* \
    && rm -rf /var/lib/apt/lists/*

EXPOSE 22

CMD ["/bin/bash", "-c", "ssh-keygen -A && exec /usr/sbin/sshd -D -e"]
