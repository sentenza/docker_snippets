# docker_base_zulujdk_11_sbt

zulu openjdk 11-latest, scala 2.13.8 and sbt 1.6.1

## Versions

```
bash-5.1# java -version
openjdk version "11.0.12" 2021-07-20 LTS
OpenJDK Runtime Environment Zulu11.50+19-CA (build 11.0.12+7-LTS)
OpenJDK 64-Bit Server VM Zulu11.50+19-CA (build 11.0.12+7-LTS, mixed mode)
bash-5.1# protoc --version
libprotoc 3.15.7
```

## Build and run the image

```
docker build -t "zulu_openjdk_11:jdk11.0.12_sbt1.6.1" .
docker run --entrypoint sh -it docker_base_zulujdk_11_sbt:jdk11.0.12_sbt1.5.6
```

## Test the image locally against an actual sbt project
At first you have to export you current sbt project that you want to test within this Docker image:

```
git archive "<GIT-BRANCH>" | gzip > your_project.tar.gz
```

Copy the tarball into this folder and use the Docker [ADD command]

```
COPY build.sbt .
// Add the project into your container:
ADD your_project.tar.gz /root/your_project
RUN ./sbt/bin/sbt sbtVersion compile && rm build.sbt
```

Run the container and then compile the project

```
docker run --entrypoint bash -it docker_base_zulujdk_11_sbt:jdk11.0.12_sbt1.5.6
```


