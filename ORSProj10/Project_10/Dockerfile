# Stage 1: Build the Spring Boot app
FROM maven:3.9.4-eclipse-temurin-17 AS build

# Set working directory
WORKDIR /app

# Copy pom.xml first (for dependency caching)
COPY pom.xml .

# Copy source code
COPY src ./src

# Ensure Spring Boot plugin is used (jar profile optional)
RUN mvn clean package -DskipTests

# Stage 2: Run the built JAR
FROM eclipse-temurin:17-jdk

# Set working directory
WORKDIR /app

# Copy the built JAR from the first stage
COPY --from=build /app/target/*.jar app.jar

# Expose backend port
EXPOSE 8084

# Run the Spring Boot app
ENTRYPOINT ["java", "-jar", "app.jar"]