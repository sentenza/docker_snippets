FROM azul/zulu-openjdk:11

ENV SCALA_VERSION 2.13.8
ENV SBT_VERSION 1.6.1

WORKDIR /root

#SHELL ["/bin/bash", "-c"]

RUN \
    apt-get -qq update && \
    apt-get install -yqq \
    wget  \
    curl \
    protobuf-compiler  \
    python3  \
    python3-pip \
    jq \
    postgresql-client \
    openssl

RUN \
  pip install awscli && \
  wget "https://downloads.typesafe.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.tgz" && \
  tar -zxf "scala-${SCALA_VERSION}.tgz" && \
  rm scala-${SCALA_VERSION}.tgz && \
  echo >> /root/.bashrc && \
  echo 'export PATH=~/scala-$SCALA_VERSION/bin:$PATH' >> /root/.bashrc

RUN \
  wget https://github.com/sbt/sbt/releases/download/v$SBT_VERSION/sbt-$SBT_VERSION.tgz && \
  tar -zxf sbt-$SBT_VERSION.tgz && \
  rm sbt-$SBT_VERSION.tgz && \
  echo >> /root/.bashrc && echo 'export PATH=/root/sbt/bin:$PATH' >> /root/.bashrc

COPY build.sbt .
#ADD trip.tar.gz /root/trip
#ADD env.sh /root/env.sh
RUN ./sbt/bin/sbt sbtVersion compile && rm build.sbt
