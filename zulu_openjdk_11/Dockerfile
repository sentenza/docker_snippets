FROM azul/zulu-openjdk:11

ENV SCALA_VERSION 2.13.10
ENV SBT_VERSION 1.8.0

WORKDIR /etc

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
    openssl \
    docker.io

RUN \
  pip install awscli && \
  wget "https://downloads.typesafe.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.tgz" && \
  tar -zxf "scala-${SCALA_VERSION}.tgz" && \
  rm scala-${SCALA_VERSION}.tgz && \
  echo >> /etc/bash.bashrc && \
  echo 'export PATH=/etc/scala-$SCALA_VERSION/bin:$PATH' >> /etc/bash.bashrc

RUN \
  wget https://github.com/sbt/sbt/releases/download/v$SBT_VERSION/sbt-$SBT_VERSION.tgz && \
  tar -zxf sbt-$SBT_VERSION.tgz && \
  rm sbt-$SBT_VERSION.tgz && \
  echo >> /etc/bash.bashrc && echo 'export PATH=/etc/sbt/bin:$PATH' >> /etc/bash.bashrc

COPY build.sbt .
#ADD trip.tar.gz /root/trip
#ADD env.sh /root/env.sh
RUN ./sbt/bin/sbt sbtVersion compile && rm build.sbt
