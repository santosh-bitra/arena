FROM ubuntu:18.04

RUN apt-get update
RUN apt-get -qy full-upgrade
RUN apt-get install -y openssh-server && \
    sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd && \
    mkdir -p /var/run/sshd && \
    apt-get install -qy openjdk-8-jdk && \
    apt-get install -qy maven && \
    apt-get -qy autoremove && \
    apt-get install -qy vim

RUN adduser --quiet jenkins && \
    echo "jenkins:1234" | chpasswd && \
    mkdir /home/jenkins/.m2
#RUN echo "jenkins:jenkins" | chpasswd &&
#RUN useradd -r jenkins



#RUN mkdir /home/remote_user/.ssh
#RUN chmod 700 /home/remote_user/.ssh

COPY remote-key.pub /home/jenkins/.ssh/authorized_keys

RUN chown -R jenkins:jenkins /home/jenkins/.m2/
RUN chown -R jenkins:jenkins /home/jenkins/.ssh/
RUN chmod 640 /home/jenkins/.ssh/authorized_keys

EXPOSE 22

#USER jenkins

CMD ["/usr/sbin/sshd", "-D"]
#CMD /usr/bin/sshd-keygen
#CMD /usr/sbin/sshd -D

#USER remote_user
#https://github.com/bibinwilson/jenkins-docker-slave/blob/master/Dockerfile