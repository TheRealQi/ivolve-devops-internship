# Docker Lab 1: Run Java Spring Boot App in a Container

This lab demonstrates how to containerize a **Spring Boot** application using **Docker**, build a Docker image, run a container, and test the application.

---

## Tasks Overview

- Clone the application code: https://github.com/Ibrahim-Adel15/Docker-1.git
- Write a `Dockerfile`.
  - Use Maven base image with Java 17
  - Create a working directory
  - Copy the application source code into the container
  - Build the app using `mvn package`
  - Run the app using the JAR file located at `target/demo-0.0.1-SNAPSHOT.jar`
  - Expose port `8080`
- Build the Docker image (`app1`).
- Run a container (`container1`) from the image.
- Test the application.
- Stop and delete the container.

---

## Steps and Screenshots

### 1. Clone the Application Code

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
```

![Clone Spring Boot App](screenshots/3.1.png)

---

### 2. Create the Dockerfile

Create a file named `Dockerfile` with the following content:

```dockerfile
FROM maven:3.9.12-eclipse-temurin-17-alpine

WORKDIR /app
COPY ./Docker-1/ .

RUN mvn package

EXPOSE 8080

CMD ["java", "-jar", "target/demo-0.0.1-SNAPSHOT.jar"]
```
---

### 3. Build the Docker Image

```bash
docker build -t app1 .
```

![Build Docker Image](screenshots/3.2.png)

---

### 4. Run the Container

```bash
docker run -d -p 8080:8080 --name container1 app1
```
---

### 5. Test the Application

Open a browser and navigate to:

```
http://localhost:8080
```
![Test Application](screenshots/3.3.png)

---

### 6. Stop and Delete the Container

```bash
docker stop container1
docker rm container1
```
