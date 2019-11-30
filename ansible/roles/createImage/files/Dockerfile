FROM java:8-jdk-alpine

COPY spring-boot.jar /usr/app/

WORKDIR /usr/app

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "spring-boot.jar"]
