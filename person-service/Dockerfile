# Build stage
FROM maven:3.9.6-eclipse-temurin-21 AS build
WORKDIR /workspace

# Copy only what this module needs
COPY person-service/pom.xml ./pom.xml
COPY person-service/src ./src

# Build this module as a standalone project
RUN mvn -B -DskipTests clean package

# Runtime stage
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY --from=build /workspace/target/*.jar app.jar
EXPOSE 80
ENV SERVER_PORT=80
ENTRYPOINT ["java","-jar","app.jar"]
