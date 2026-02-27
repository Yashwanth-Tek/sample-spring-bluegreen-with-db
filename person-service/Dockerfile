FROM alpine:3.20 AS build
WORKDIR /build
COPY target/*.jar app.jar

FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY --from=build /build/app.jar app.jar

EXPOSE 80
ENV SERVER_PORT=80
ENTRYPOINT ["java", "-jar", "app.jar"]
