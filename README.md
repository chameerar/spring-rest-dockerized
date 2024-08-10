# Dockerizing a Spring Boot Application

This project demonstrates how to containerize a Spring Boot application using Docker. The Dockerfile provided allows you to build and run a Spring Boot application in a Docker container, ensuring consistent environments for development, testing, and production.

## Project Structure
```
.
├── src/ # Source code of the Spring Boot application
├── pom.xml # Maven project configuration file
└── Dockerfile # Dockerfile for building the Docker image
```
## Prerequisites

- [Docker](https://www.docker.com/get-started) installed on your machine.

## Dockerfile Overview

This project uses a multi-stage Dockerfile to build and package the Spring Boot application:

1. **Build Stage**:
   - Uses the `maven:3.8.3-openjdk-17` image to build the project.
   - Copies the source code and `pom.xml` into the container.
   - Runs `mvn clean package` to build the JAR file.

2. **Package Stage**:
   - Uses the `openjdk:17` image to create a lightweight container.
   - Copies the JAR file from the build stage into the container.
   - Exposes port `8080`.
   - Sets the user to `10014` for running the application.
   - Defines the entry point to run the Spring Boot application using the JAR file.
  
## Building the Docker Image
To build the Docker image, navigate to the directory containing the Dockerfile and run the following command:
```bash
docker build -t springboot-docker .
```

## Running the Docker Container
After building the Docker image, you can run the container using:

```bash
docker run -d -p 8080:8080 springboot-docker
```
This command will run the Spring Boot application in a Docker container and map port 8080 of the container to port 8080 on your host machine.

## Testing the Application
The application includes a simple REST controller that responds with a "Hello World" message. To test the application:

1. Open your web browser or use a tool like curl or Postman.
2. Navigate to the following URL:
```
http://localhost:8080/hello/message
```
3. You should see the following response:
```
Hello World
```
This confirms that the application is running successfully in the Docker container.
