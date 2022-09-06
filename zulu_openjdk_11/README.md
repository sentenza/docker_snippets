# Zulu Openjdk 11-latest (Ubuntu) 

zulu openjdk 11-latest (11.0.16+), scala 2.13.8 and sbt 1.7.1

## Versions

```
bash-5.1# java -version
openjdk version "11.0.16.1" 2022-07-19 LTS
OpenJDK Runtime Environment Zulu11.58+23-CA (build 11.0.16.1+1-LTS)
OpenJDK 64-Bit Server VM Zulu11.58+23-CA (build 11.0.16.1+1-LTS, mixed mode)
```

## Build and run the image

```
docker build -t "zulu_openjdk:jdk11_sbt171" .
docker run --entrypoint /bin/bash -it zulu_openjdk:jdk11_sbt171
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
docker run --entrypoint bash -it zulu_openjdk:jdk11_sbt171
```


