# stage 1
FROM maven:3.9.5-amazoncorretto-17 AS build 
WORKDIR /shipping
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn clean package -DskipTests

# stage 2
FROM amazoncorretto:17-jre-alpine
WORKDIR /shipping
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
RUN chown roboshop:roboshop /shipping
USER roboshop
EXPOSE 8080
ENV CART_ENDPOINT=cart:8080 DB_HOST=mysql
COPY --from=build /shipping/target/shipping-1.0.jar ./shipping.jar
# Use JRE arguments to optimize memory usage (Crucial for microservices)
CMD [ "java", "-XX:+ExitOnOutOfMemoryError", "-XX:MaxRAMPercentage=80.0", "-jar", "shipping.jar" ]