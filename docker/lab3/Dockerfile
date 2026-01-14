FROM maven:3.9.12-eclipse-temurin-17-alpine AS build

WORKDIR /app

COPY . .

RUN mvn package


FROM eclipse-temurin:17-jre-alpine

WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]
