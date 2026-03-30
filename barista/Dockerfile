FROM gradle:6-jdk8  AS builder

COPY --chown=gradle:gradle . .

RUN cd barista && gradle build --no-daemon

FROM sdaschner/wildfly:javaee8-kafka-b1

RUN sed -i 's/<resource-root path="slf4j-api-1.7.25.jar"\/>//g' /opt/jboss/wildfly/modules/org/apache/kafka/clients/main/module.xml && \
    sed -i 's/<dependencies>/<dependencies><module name="org.slf4j"\/><module name="org.slf4j.impl"\/>/g' /opt/jboss/wildfly/modules/org/apache/kafka/clients/main/module.xml

COPY --from=builder /home/gradle/barista/build/libs/barista.war $DEPLOYMENT_DIR
EXPOSE 8080
