#Construcción (Multi-stage)
FROM maven:3.9-eclipse-temurin-17 AS builder
WORKDIR /app

COPY Springboot-API-REST/pom.xml .
COPY Springboot-API-REST/src ./src

RUN mvn clean package -DskipTests

#Ejecución
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

# Mínimo Privilegio
RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring

# Copia
COPY --from=builder /app/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]