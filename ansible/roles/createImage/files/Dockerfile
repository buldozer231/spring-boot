FROM java:8-jdk-alpine

COPY spring-boot-smoke-test-web-ui-2.2.1.BUILD-SNAPSHOT.jar /usr/app/

WORKDIR /usr/app

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "spring-boot-smoke-test-web-ui-2.2.1.BUILD-SNAPSHOT.jar"]
