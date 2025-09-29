# Stage 1: Build backend JAR
FROM maven:3.8.6-openjdk-8 AS builder
WORKDIR /app

# Copy root POM and backend module
COPY pom.xml ./pom.xml
COPY backend/pom.xml ./backend/pom.xml
COPY backend/src ./backend/src

# Build backend using the parent POM
WORKDIR /app/backend
RUN mvn clean package -DskipTests

# Stage 2: Runtime image
FROM openjdk:8
WORKDIR /app

# Copy the built backend JAR
COPY --from=builder /app/backend/target/backend-1.0-RELEASE.jar backend.jar

EXPOSE 8080
CMD ["java", "-jar", "backend.jar"]
