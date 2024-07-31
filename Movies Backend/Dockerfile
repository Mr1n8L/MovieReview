# Use the official Maven image to build the app
FROM maven:3.8.5-openjdk-17 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the pom.xml and download the dependencies
COPY pom.xml ./
RUN mvn dependency:go-offline -B

# Copy the source code
COPY src ./src

# Package the application
RUN mvn clean package -DskipTests

# Use the official OpenJDK image to run the app
FROM openjdk:17-jdk-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the packaged jar file from the build stage
COPY --from=build /app/target/movies-0.0.1-SNAPSHOT.jar app.jar

# Expose the port the app runs on
EXPOSE 8080

# Define the command to run the app
ENTRYPOINT ["java", "-jar", "app.jar"]
