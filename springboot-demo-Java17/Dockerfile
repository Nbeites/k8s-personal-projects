FROM openjdk:17-jdk-alpine
ARG WAR_FILE
COPY ${WAR_FILE} /springboot-demo.war
ENTRYPOINT ["java", "-jar", "/app.war"]