FROM maven:3.9.6-eclipse-temurin-21 AS builder
WORKDIR /app
# Copy parent pom first
COPY pom.xml .
# Copy service
COPY swift-userService/pom.xml swift-userService/
COPY swift-userService/src swift-userService/src
# Build from root so parent pom is available
RUN mvn -pl swift-userService -am clean package -DskipTests

FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY --from=builder /app/swift-userService/target/*.jar app.jar
EXPOSE 8081
ENTRYPOINT ["java", "-jar", "app.jar"]