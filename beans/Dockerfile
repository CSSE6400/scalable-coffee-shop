FROM gradle:6-jdk8  AS builder

COPY --chown=gradle:gradle . .

RUN cd beans && gradle build --no-daemon

FROM sdaschner/wildfly:javaee8-kafka-b1

COPY --from=builder /home/gradle/beans/build/libs/beans.war $DEPLOYMENT_DIR
EXPOSE 8080
