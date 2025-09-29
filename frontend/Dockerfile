# Stage 1: Build frontend JAR
FROM maven:3.8.6-openjdk-8 AS builder
WORKDIR /app

# Copy root POM and frontend module
COPY pom.xml ./pom.xml
COPY frontend/pom.xml ./frontend/pom.xml
COPY frontend/src ./frontend/src

# Build frontend using the parent POM
WORKDIR /app/frontend
RUN mvn clean package -DskipTests

# Stage 2: Runtime image
FROM openjdk:8
WORKDIR /app

# Copy the built frontend JAR and web resources
COPY --from=builder /app/frontend/target/frontend-1.0-RELEASE.jar frontend.jar
COPY frontend/src/main/webapp/ src/main/webapp/

EXPOSE 8080
CMD ["java", "-Dapi.host.baseurl=${BACKEND}", "-jar", "frontend.jar"]
