FROM ubuntu:12.04

RUN apt-get update

# Make it easy to install PPA sources
RUN apt-get install -y python-software-properties

# Install Oracle's Java (Recommended for Hadoop)
# Auto-accept the license
RUN add-apt-repository -y ppa:webupd8team/java
RUN apt-get update
RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
RUN apt-get -y install oracle-java7-installer
ENV JAVA_HOME /usr/lib/jvm/java-7-oracle
