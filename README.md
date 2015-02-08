hadoop-docker
=============

Hadoop inside Docker. 



Building
========

Hadoop and Hadoop-dev depend on oracle7. You can build everything yourself
easily, but update the Dockerfiles to change the 'FROM' field to your tag, 
which is probably `<yourname>/oracle-java7`

    $ git clone https://github.com/hamiltont/hadoop-docker.git
    $ cd hadoop-docker/oracle-java7
    $ sudo docker build -t <yourname>/oracle-java7 .
    $ cd ../hadoop-dev
    $ sudo docker build -t <yourname>/hadoop-dev .
    $ CONT=$(sudo docker run -d <yourname>/hadoop-dev /bin/bash -c "exit")
    $ sudo docker cp ${CONT}:/tmp/hadoop-2.2.0-src/hadoop-dist/target/hadoop-2.2.0.tar.gz ../hadoop
    $ cd ../hadoop
    $ sudo docker build -t <yourname>/hadoop . 
