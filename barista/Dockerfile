FROM gradle:4.7.0-jdk8-alpine AS builder

COPY --chown=gradle:gradle . .

RUN cd barista && gradle build --no-daemon

FROM sdaschner/wildfly:javaee8-kafka-b1

COPY --from=builder /home/gradle/barista/build/libs/barista.war $DEPLOYMENT_DIR
EXPOSE 8080
