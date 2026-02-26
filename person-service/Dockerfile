# Build stage
FROM maven:3.9.6-eclipse-temurin-21 AS build
WORKDIR /workspace

# Copy root pom + module pom first (better caching)
COPY pom.xml ./pom.xml
COPY person-service/pom.xml ./person-service/pom.xml

# Copy the module source
COPY person-service/src ./person-service/src

# Build only the module (still uses parent pom)
RUN mvn -B -DskipTests -pl person-service -am clean package

# Runtime stage
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY --from=build /workspace/person-service/target/*.jar app.jar
EXPOSE 80
ENV SERVER_PORT=80
ENTRYPOINT ["java","-jar","app.jar"]
