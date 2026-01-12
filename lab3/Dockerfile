FROM maven:3.9.12-eclipse-temurin-17-alpine

WORKDIR /app
COPY ./Docker-1/ .

RUN mvn package

EXPOSE 8080

CMD ["java", "-jar", "target/demo-0.0.1-SNAPSHOT.jar"]

