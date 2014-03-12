FROM hamiltont/oracle-java7

RUN apt-get update

# If you built the hadoop-dev container then it generates this .tar.gz
# docker cp can be used to pull it to your host filesystem
ADD hadoop-2.2.0.tar.gz /

RUN mkdir /hadoop
ADD hadoop-2.2.0.tar.gz /tmp/
RUN tar -xzvf /hadoop/hadoop-2.2.0.tar.gz -C /hadoop --strip-components 1

# Download/setup Hadoop's SSH dependency
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN ssh-keygen -t rsa -P "" -f /root/.ssh/id_rsa
RUN cat /root/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys
  
# Manually accept host verification key
RUN /usr/sbin/sshd && \
  ssh -o StrictHostKeyChecking=no localhost exit &&\
  ssh -o StrictHostKeyChecking=no 0.0.0.0 exit   &&\
  ssh -o StrictHostKeyChecking=no 127.0.0.1 exit

# Ensure hadoop workers that SSH into root@localhost can still find Java
RUN echo "export JAVA_HOME=$JAVA_HOME" > /tmp/tmp_profile && \
  cat /root/.bashrc >> /tmp/tmp_profile && \
  mv /tmp/tmp_profile /root/.bashrc
  
# Setup up supervisor 
RUN apt-get install -y supervisor &&\
  mkdir -p /var/log/supervisor
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD ["/usr/bin/supervisord"]
