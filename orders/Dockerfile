FROM gradle:4.7.0-jdk8-alpine AS builder

COPY --chown=gradle:gradle . .

RUN cd orders && gradle build --no-daemon

FROM sdaschner/wildfly:javaee8-kafka-b1

COPY --from=builder /home/gradle/orders/build/libs/orders.war $DEPLOYMENT_DIR
EXPOSE 8080
