# docker_base_zulujdk_11_sbt

zulu openjdk 11.0.12, scala 2.13.7 and sbt 1.5.5

## Build and run the image

```
docker build -t "docker_base_zulujdk_11_sbt:jdk11.0.12_sbt1.5.5" .
docker run --entrypoint sh -it docker_base_zulujdk_11_sbt:jdk11.0.12_sbt1.5.5
```
