FROM docker:latest
ENV LANG C.UTF-8 

ENV SCALA_VERSION 2.13.2
ENV SBT_VERSION 1.3.12

RUN apk add --update \
    python \
    python-dev \
    py-pip \
    build-base \
    postgresql-client \
    postgresql-dev \
    curl \
    wget \
    bash \
    jq \
    openssl \
  && rm -rf /var/cache/apk/*

RUN ZULU_ARCH=zulu14.28.21-ca-jdk14.0.1-linux_musl_x64.tar.gz && \
    INSTALL_DIR=/usr/lib/jvm && \
	BIN_DIR=/usr/bin && \
	MAN_DIR=/usr/share/man/man1 && \
	ZULU_DIR=$( basename ${ZULU_ARCH} .tar.gz ) && \
	wget -q https://cdn.azul.com/zulu/bin/${ZULU_ARCH} && \
	mkdir -p ${INSTALL_DIR} && \
	tar -xf ./${ZULU_ARCH} -C ${INSTALL_DIR} && rm -f ${ZULU_ARCH} && \
	cd ${BIN_DIR} && find ${INSTALL_DIR}/${ZULU_DIR}/bin -type f -perm -a=x -exec ln -s {} . \; && \
	mkdir -p ${MAN_DIR} && \
	cd ${MAN_DIR} && find ${INSTALL_DIR}/${ZULU_DIR}/man/man1 -type f -name "*.1" -exec ln -s {} . \; && \
	java -version

WORKDIR /root

RUN \
  pip install awscli && \
  wget "https://downloads.typesafe.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.tgz" && \
  tar -zxf "scala-${SCALA_VERSION}.tgz" && \
  echo >> /root/.bashrc && \
  echo 'export PATH=~/scala-$SCALA_VERSION/bin:$PATH' >> /root/.bashrc

RUN \
  curl -L -o sbt-$SBT_VERSION.tgz https://github.com/sbt/sbt/releases/download/v$SBT_VERSION/sbt-$SBT_VERSION.tgz && \
  tar -zxf sbt-$SBT_VERSION.tgz && \
  echo >> /root/.bashrc && echo 'export PATH=/root/sbt/bin:$PATH' >> /root/.bashrc

COPY build.sbt .
RUN ./sbt/bin/sbt sbtVersion compile && rm build.sbt
