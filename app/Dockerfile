FROM openjdk:11.0.7-jdk-slim
VOLUME /tmp
ADD  build/libs/demo-0.0.1-SNAPSHOT.jar app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
