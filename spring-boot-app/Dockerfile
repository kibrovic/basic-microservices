FROM maven:3-jdk-8-alpine

# install necessary tools
RUN apk add --no-cache git

# clone repo in /tmp/ directory
RUN git clone https://github.com/kkenan/basic-microservices.git /tmp/basic-microservices

# set working directory to spring-boot-app
WORKDIR /tmp/basic-microservices/spring-boot-app

# resolve maven dependencies and package the code
RUN ["mvn", "dependency:resolve"]
RUN ["mvn", "clean", "package"]

# add custom springboot configs
ADD my-conf.yml /tmp/basic-microservices/spring-boot-app/my-conf.yml

EXPOSE 8080

# set startup cmd to execute jar
CMD ["java", "-jar", "target/spring-boot-app-1.0-SNAPSHOT.jar", "--spring.config.location=my-conf.yml"]
