FROM ubuntu:18.04

RUN apt-get update
RUN apt-get install -y openssh-server
RUN useradd -r remote_user --password 1234 -m

#USER remote_user

RUN mkdir /home/remote_user/.ssh
RUN chmod 700 /home/remote_user/.ssh

COPY remote-key.pub /home/remote_user/.ssh/authorized_keys

RUN chown remote_user -R /home/remote_user/.ssh/
RUN chmod 600 /home/remote_user/.ssh/authorized_keys

USER remote_user

CMD /usr/bin/sshd-keygen
CMD /usr/sbin/sshd -D

#USER remote_user
