FROM openjdk:11.0.1-jdk
ENV LANG C.UTF-8

ENV SCALA_VERSION 2.12.8
ENV SBT_VERSION 1.2.7

RUN apt-get update && apt-get install -y --no-install-recommends \
    python-setuptools \
    python-dev \
    python-pip \
    libpython-dev \
    postgresql-client \
    curl \
    bash \
    jq \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /root

RUN \
  pip install awscli && \
  curl -fsL https://downloads.typesafe.com/scala/$SCALA_VERSION/scala-$SCALA_VERSION.tgz | tar xfz - -C /root/ && \
  echo >> /root/.bashrc && \
  echo 'export PATH=~/scala-$SCALA_VERSION/bin:$PATH' >> /root/.bashrc

RUN \
  curl -L -o sbt-$SBT_VERSION.tgz https://github.com/sbt/sbt/releases/download/v$SBT_VERSION/sbt-$SBT_VERSION.tgz && tar -zxf sbt-$SBT_VERSION.tgz && \
  echo >> /root/.bashrc && echo 'export PATH=/root/sbt/bin:$PATH' >> /root/.bashrc

RUN ./sbt/bin/sbt sbtVersion
