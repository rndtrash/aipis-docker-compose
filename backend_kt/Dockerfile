FROM gradle:jdk17 AS build
COPY --chown=gradle:gradle ./Backend_time_manager_events /var/build-backend-kt
WORKDIR /var/build-backend-kt
RUN gradle build -x test

FROM eclipse-temurin:17
# ENV DB_URL=jdbc:postgresql://localhost:5432/backend-time-manager-events
RUN mkdir -p /var/backend-kt
COPY --from=build /var/build-backend-kt/build/libs/application-0.0.1-SNAPSHOT.jar /var/backend-kt
RUN bash -c 'touch /var/backend-kt/application-0.0.1-SNAPSHOT.jar'
WORKDIR /var/backend-kt
ENTRYPOINT exec java -XX:+UnlockExperimentalVMOptions -XX:+UseContainerSupport -Djava.security.egd=file:/dev/./urandom -jar /var/backend-kt/application-0.0.1-SNAPSHOT.jar --spring.datasource.url="$DB_URL" --server.port="$PORT"
