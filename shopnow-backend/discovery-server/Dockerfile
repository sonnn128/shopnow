FROM maven:3.8.3-openjdk-17 AS build
WORKDIR /app
COPY . .
RUN mvn install -DskipTests=true

FROM eclipse-temurin:17.0.8.1_1-jre-ubi9-minimal

RUN unlink /etc/localtime;ln -s  /usr/share/zoneinfo/Asia/Ho_Chi_Minh /etc/localtime
COPY --from=build app/target/discovery-server-0.0.1-SNAPSHOT.war /run/discovery-server-0.0.1-SNAPSHOT.war

EXPOSE 8761

ENV JAVA_OPTIONS="-Xmx2048m -Xms256m"
# ENTRYPOINT ["java", "-jar", "/run/discovery-server-0.0.1-SNAPSHOT.war"] --spring.config.location=/app/src/main/resources/application.properties
ENTRYPOINT exec java -jar /run/discovery-server-0.0.1-SNAPSHOT.war --spring.config.location=/run/src/main/resources/application.properties
