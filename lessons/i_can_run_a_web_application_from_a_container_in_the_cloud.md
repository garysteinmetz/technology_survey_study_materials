# I Can Run a Web Application from a Container in the Cloud

create a boot Jar

running the boot Jar

'fat Jar'

run a Docker image locally

https://hub.docker.com/r/adoptopenjdk/openjdk11/

docker pull adoptopenjdk/openjdk11:jdk-11.0.7_10-alpine

https://hub.docker.com/editions/community/docker-ce-desktop-mac

https://www.docker.com/products/docker-desktop

https://hub.docker.com/editions/community/docker-ce-desktop-windows

https://docs.spring.io/spring-boot/docs/current/maven-plugin/

shell script to build and run

./mvnw help:describe -Dplugin=org.springframework.boot:spring-boot-maven-plugin -Ddetail=true

clean spring-boot:repackage

./mvnw clean package spring-boot:repackage

docker container rm $(docker container ls –aq)
