# Docker Lab 3: Multi-Stage Build for a Node.js App

This lab demonstrates how to containerize a **Node.js** application using **Docker** and build a multi-stage **Dockerfile**.

---

## Tasks Overview

- Clone the Application Code https://github.com/Ibrahim-Adel15/Docker-1.git
- Build the application
- Write Dockerfile with Multi-stage.
  - Use Maven base image for first stag
  - Copy the application code into the container
  - Build the app using mvn package
  - Copy JAR file from first stag
  - Expose port `8080`
  - Run the app
- Build app3 Image (Note the image size).
- Run container3 from app3 image.
- Test the application.
- Stop and delete the container.

---

## Steps and Screenshots

### 1. Clone the Application Code

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
```

![Clone the Application](screenshots/1.png)

---

### 2. Create the Dockerfile

Create a file named `Dockerfile` with the following content:

```dockerfile
FROM maven:3.9.12-eclipse-temurin-17-alpine AS build

WORKDIR /app
COPY . .
RUN mvn package

FROM eclipse-temurin:17-jre-alpine

WORKDIR /app
COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]
```
---

### 3. Build the Docker image

```bash
docker build -t app3 .
```
![Build Docker Image](screenshots/2.png)

---

### 4. Comparing Image Sizes from Docker Labs 1 & 2
When comparing Docker image sizes, we see that using a multi-stage Dockerfile produces an image size equivalent to the prebuilt application in Lab 2 and smaller than the single-stage Dockerfile. Unlike Lab 2, where the application had to be built manually before creating the image, the multi-stage approach automates the build and packaging process within the Docker build itself, making it more efficient and consistent.
```bash
docker images
```
![Images Sizes](screenshots/3.png)

---

### 5. Run the Container
```bash
docker run -d -p 8080:8080 --name container3 app3
```
---

### 6. Test the Application

Open a browser and navigate to:

```
http://localhost:8080
```
![Test Application](screenshots/4.png)

---

### 7. Stop and Delete the Container

```bash
docker stop container3
docker rm container3
```
