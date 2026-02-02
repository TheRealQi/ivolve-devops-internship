# Docker Lab 7:  Containerized Node.js and MySQL Stack Using Docker Compose

This lab demonstrates how to build and run frontend and backend microservices using Docker, connect containers using a custom Docker network, and verify inter-container communication.

---

## Tasks Overview

- Clone the application source code from https://github.com/Ibrahim-Adel15/kubernets-app.git
- The application requires a MySQL connection and must find a database named ivolve to start working.
- Create docker-compose.yml file with:
	- App service
		- Build from the local Dockerfile
		- Map port 3000
		- Use environment variables:
			- DB_HOST
			- DB_USER
			- DB_PASSWORD
	- DB service
		- Use MySQL image
		- Set environment variable MYSQL_ROOT_PASSWORD
	- db_data volume  for /var/lib/mysql
- Verify app is working
- Verify app /health & /ready
- Verify app access logs at /app/logs/
- Push the Docker image into your DockerHub
---
## Steps and Screenshots

### 1. Clone the Repository

Clone the repository:

```bash
git clone https://github.com/Ibrahim-Adel15/kubernets-app.git lab7
cd lab7
```
![Clone Repository](screenshots/1.png)

---
### 2. Docker Compose
#### 2.1 App Docker Compose File
Create `docker-compose.yaml` file with the following content:
```yaml
services:
  app:
    build: .
    container_name: app
    ports:
      - "8000:3000"
    environment:
      DB_HOST: db
      DB_USER: root
      DB_PASSWORD: root
    depends_on:
      - db
  db:
    image: mysql:8.0.44-debian
    container_name: db
    restart: always
    environment:
      MYSQL_DATABASE: ivolve
      MYSQL_ROOT_PASSWORD: root
    volumes:
      - db_data:/var/lib/mysql
volumes:
  db_data:
```

#### 2.2 Run Application

Build and start the services using Docker Compose:

```bash
docker compose up --build -d
```
This command:
- Builds the Node.js application image from the local `Dockerfile`
- Starts both app and db containers
- Creates a custom Docker network
![Running the Application](screenshots/2.png)

### 3. Verify
#### 3.1 Verify the Application via Browser
Open your browser and navigate to:
```
http://localhost:8000
```
The application should be running successfully indicating the app is running and can connect to the db service.
![Verifying the Application via Browser](screenshots/3.png)
#### 3.2 Verify Health and Ready Endpoints

Test the health and ready endpoints using `curl`:
```bash
curl http://localhost:8000/health
curl http://localhost:8000/ready
```
![Verifying the Health and Ready Endpoints via Curl](screenshots/4.png)
#### 3.3 Verify Application Logs
List the logs directory inside the app container:
```bash
docker exec app ls /app/logs
```
View the access logs:
```bash
docker exec app cat /app/logs/access.log
```
![](screenshots/5.png)
### 4. Push Docker Image to Docker Hub
1. Tag the locally built image:

```bash
docker tag lab7-app:latest <dockerhub-username>/app7:1.0
```
2. Push the image:
```bash
docker push <dockerhub-username>/app7:1.0
```
![](screenshots/6.png)

