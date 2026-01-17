
# Lab 1: Building and Packaging Java Applications with Gradle

This lab demonstrates building and packaging a Java application using Gradle, running unit tests, generating a build artifact, and running the application.

---

## Tasks Overview

    1. Install Gradle.
    2. Clone the source code: [https://github.com/Ibrahim-Adel15/build1.git](https://github.com/Ibrahim-Adel15/build1.git)
    3. Run unit tests.
    4. Build the application to generate the JAR artifact (`build/libs/ivolve-app.jar`).
    5. Run the application.
    6. Verify the application is working.

## Steps and Screenshots

### 1. Installing Gradle

#### 1.1 Download and Install Gradle
```bash
sudo wget services.gradle.org/distributions/gradle-8.5-bin.zip -P /tmp
sudo unzip -d /opt/gradle /tmp/gradle-8.5-bin.zip
```
#### 1.2 Configure Gradle Environment Variables
```bash
echo 'export GRADLE_HOME=/opt/gradle/gradle-8.5' >> ~/.bashrc
echo 'export PATH=$GRADLE_HOME/bin:$PATH' >> ~/.bashrc
```
#### 1.3 Verify Gradle Installation
```bash
gradle -v
```
![Verify Gradle Installation](screenshots/1.1.png)

### 2. Clone the Application Repository
```bash
git clone https://github.com/Ibrahim-Adel15/build1.git
cd build1/
```
![Cloning  App Repository](screenshots/1.2.png)

### 3. Run Unit Tests
```bash
gradle test
```
![Running Unit Tests](screenshots/1.3.png)

### 4. Build the Application
```bash
gradle build
```
![Building the Application](screenshots/1.4.png)

### 5. Run the Application
```bash
java -jar ./build/libs/ivolve-app.jar
```
![Running the Application](screenshots/1.5.png)
