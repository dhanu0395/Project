# Stage 1: Build JAR
FROM maven:3.9.0-openjdk-8 AS builder
WORKDIR /app
COPY frontend/pom.xml ./pom.xml
COPY frontend/src ./src
RUN mvn clean package -DskipTests

# Stage 2: Runtime image
FROM openjdk:8
WORKDIR /app
COPY --from=builder /app/target/frontend-1.0-RELEASE.jar frontend.jar
COPY frontend/src/main/webapp/ src/main/webapp/
EXPOSE 8080
CMD ["java", "-Dapi.host.baseurl=${BACKEND}", "-jar", "frontend.jar"]
