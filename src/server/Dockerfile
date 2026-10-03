# Start with Java 21 development tools.
FROM eclipse-temurin:21-jdk AS build

# Set the working folder inside the container.
WORKDIR /app

# Copy the server project into that folder.
COPY . .

# Make the Maven launcher executable.
RUN chmod +x mvnw

# Download dependencies, compile, run tests, and create the JAR.
RUN ./mvnw -B package

# Start a smaller environment with Java 21's runtime.
FROM eclipse-temurin:21-jre

WORKDIR /app

# Copy the built JAR into the runtime environment.
COPY --from=build /app/target/*.jar app.jar

# Start the application.
ENTRYPOINT ["java", "-jar", "app.jar"]