# Stage 1: Build JAR
FROM maven:3.9.0-openjdk-8 AS builder
WORKDIR /app
COPY backend/pom.xml ./pom.xml
COPY backend/src ./src
RUN mvn clean package -DskipTests

# Stage 2: Runtime image
FROM openjdk:8
WORKDIR /app
COPY --from=builder /app/target/backend-1.0-RELEASE.jar backend.jar
EXPOSE 8080
CMD ["java", "-jar", "backend.jar"]
