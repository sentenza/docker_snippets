# Docker snippets.

Just a bunch of docker file we needed over time.

## docker_base_zulujdk_11_sbt

At the moment the base image is using Alpine Linux and Azul JDK and precisely zulu11.50.19 JDK 11.0.12 also described here https://docs.azul.com/core/zulu-openjdk/release-notes/october-2021

The full list of images available can be seen here https://cdn.azul.com/zulu/bin/ and we are using https://cdn.azul.com/zulu/bin/zulu11.50.19-ca-jdk11.0.12-linux_musl_x64.tar.gz

## docker_base_openjdk_8_sbt

Is openjdk 8 that needed docker:latest as the base image

## docker_base_ruby

Ruby 2.3 that needed docker:latest as base


## docker_mongodb_2

Mongodb 2.6 image
