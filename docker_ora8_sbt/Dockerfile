# Pull base image
FROM sgrio/java-oracle:jdk_8
MAINTAINER Charles Lee <docker@charleetm.org>

ENV SCALA_VERSION 2.11.7
ENV SBT_VERSION 1.0.2

RUN apt-get update -y && apt-get install python-pip -y && apt-get install -y postgresql postgresql-client libpq-dev

# Install Scala
## Piping curl directly in tar
RUN \
  curl -fsL https://downloads.typesafe.com/scala/$SCALA_VERSION/scala-$SCALA_VERSION.tgz | tar xfz - -C /root/ && \
  echo >> /root/.bashrc && \
  echo 'export PATH=~/scala-$SCALA_VERSION/bin:$PATH' >> /root/.bashrc

WORKDIR /root

RUN \
  curl -L -o sbt-$SBT_VERSION.tgz https://github.com/sbt/sbt/releases/download/v$SBT_VERSION/sbt-$SBT_VERSION.tgz && tar -zxf sbt-$SBT_VERSION.tgz && \
  echo >> /root/.bashrc && echo 'export PATH=/root/sbt/bin:$PATH' >> /root/.bashrc

RUN ./sbt/bin/sbt sbtVersion
