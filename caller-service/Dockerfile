# Build stage
FROM maven:3.9-eclipse-temurin-21 AS build
WORKDIR /app

# Copy parent pom first
COPY ../pom.xml /app/parent/pom.xml

# Copy caller-service pom and source
COPY pom.xml .
COPY src ./src

# Build the application
RUN mvn clean package -DskipTests -f /app/pom.xml

# Runtime stage
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app

# Copy the built jar from build stage
COPY --from=build /app/target/*.jar app.jar

# Expose port 80
EXPOSE 80

# Set server port to 80
ENV SERVER_PORT=80

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
