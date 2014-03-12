FROM hamiltont/oracle-java7

RUN apt-get update

# Needed to download Hadoop release from Apache website
RUN apt-get install -y wget

# Download and build Hadoop's protobuf dependency
RUN apt-get install -y zlib1g-dev autoconf automake build-essential maven cmake libssl-dev
RUN wget http://protobuf.googlecode.com/files/protobuf-2.5.0.tar.gz
RUN tar -xzvf protobuf-2.5.0.tar.gz -C /tmp &&\
  cd /tmp/protobuf-2.5.0 && \
  ./configure && \
  make && make install && \
  ldconfig

# Download build Hadoop
RUN wget http://apache.mirrors.tds.net/hadoop/common/hadoop-2.2.0/hadoop-2.2.0-src.tar.gz
RUN tar -xvzf hadoop-2.2.0-src.tar.gz -C /tmp && \
  cd /tmp/hadoop-2.2.0-src

# Minor patch needed for compilation
ADD hadoop-auth-pom.xml.patch /tmp/hadoop-auth-pom.xml.patch
RUN patch /tmp/hadoop-2.2.0-src/hadoop-common-project/hadoop-auth/pom.xml /tmp/hadoop-auth-pom.xml.patch

# Build Hadoop (also builds native 64-bit library)
RUN cd /tmp/hadoop-2.2.0-src && \
  mvn package -Pdist,native -DskipTests -Dtar

# Move the tar into a standard location for extraction from container
# RUN mv /tmp/hadoop-2.2.0-src/hadoop-dist/target/hadoop-2.2.0.tar.gz 
