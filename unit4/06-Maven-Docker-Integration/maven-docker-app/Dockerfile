FROM amazoncorretto:8

WORKDIR /app

COPY target/maven-docker-app-1.0-SNAPSHOT.jar app.jar

CMD ["java","-jar","app.jar"]