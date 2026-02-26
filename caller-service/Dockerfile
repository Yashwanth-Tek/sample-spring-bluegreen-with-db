# Build stage
FROM maven:3.9.6-eclipse-temurin-21 AS build
WORKDIR /workspace

# copy parent pom (for parent resolution) + module sources
COPY pom.xml ./pom.xml
COPY person-service/pom.xml ./person-service/pom.xml
COPY person-service/src ./person-service/src

# build ONLY the module (doesn't require other modules' folders)
RUN mvn -B -DskipTests -f person-service/pom.xml clean package

# Runtime stage
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY --from=build /workspace/person-service/target/*.jar app.jar
EXPOSE 80
ENV SERVER_PORT=80
ENTRYPOINT ["java","-jar","app.jar"]
