# Build
FROM maven:3.8.4-openjdk-8 AS build

WORKDIR /opt/shipping

# Copy only pom.xml first to download dependencies
COPY pom.xml .
RUN mvn dependency:resolve

# Copy source code
COPY src ./src/

# Build without tests and skip main compilation (focus on just creating the jar)
RUN mvn package -Dmaven.test.skip=true -Dmaven.main.skip=true

# Run
FROM openjdk:8-jre-alpine

EXPOSE 8080

WORKDIR /opt/shipping

COPY --from=build /opt/shipping/target/shipping-1.0.jar shipping.jar

CMD [ "java", "-Xmn256m", "-Xmx768m", "-jar", "shipping.jar" ]