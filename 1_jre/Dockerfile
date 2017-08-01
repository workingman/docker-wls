FROM oraclelinux:7-slim

ENV JAVA_HOME=/usr/java/default

ADD server-jre-8u*-linux-x64.tar.gz /usr/java/

RUN export JAVA_DIR=/usr/java/jdk1.8.0_131 && \
    echo "$JAVA_DIR" > /root/javadir && \
    ln -s $JAVA_DIR /usr/java/latest && \
    ln -s $JAVA_DIR /usr/java/default && \
    alternatives --install /usr/bin/java java $JAVA_DIR/bin/java 20000 && \
    alternatives --install /usr/bin/javac javac $JAVA_DIR/bin/javac 20000 && \
    alternatives --install /usr/bin/jar jar $JAVA_DIR/bin/jar 20000
