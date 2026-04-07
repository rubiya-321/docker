FROM maven:3.9.14 AS builder
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package && \
    mv target/shipping-1.0.jar shipping.jar 

FROM eclipse-temurin:17-jre-alpine
EXPOSE 8080
WORKDIR /app
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /app
COPY --from=builder /app/shipping.jar .
USER roboshop
ENTRYPOINT ["java", "-jar", "shipping.jar"]