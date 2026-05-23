#Construcción
FROM maven:3.9-eclipse-temurin-17 AS builder
WORKDIR /app
COPY Springboot-API-REST-DESPACHO/pom.xml .
COPY Springboot-API-REST-DESPACHO/src ./src
RUN mvn clean package -DskipTests

#Ejecución
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring
COPY --from=builder /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]