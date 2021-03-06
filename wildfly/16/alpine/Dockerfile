# This Dockerfile is strongly based on jboss/wildfly docker definition.

FROM adoptopenjdk/openjdk11:alpine

RUN apk add --update curl && \
    rm -rf /var/cache/apk/*

# Set the WILDFLY_VERSION env variable
ENV WILDFLY_VERSION 16.0.0.Final
ENV WILDFLY_SHA1 287c21b069ec6ecd80472afec01384093ed8eb7d
ENV JBOSS_HOME /opt/wildfly

USER root

# Add the WildFly distribution to /opt, and make wildfly the owner of the extracted tar content
# Make sure the distribution is available from a well-known place
RUN cd $HOME \
    && curl -O https://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.tar.gz \
    && sha1sum wildfly-$WILDFLY_VERSION.tar.gz | grep $WILDFLY_SHA1 \
    && tar xf wildfly-$WILDFLY_VERSION.tar.gz \
    && mv $HOME/wildfly-$WILDFLY_VERSION $JBOSS_HOME \
    && rm wildfly-$WILDFLY_VERSION.tar.gz

# Ensure signals are forwarded to the JVM process correctly for graceful shutdown
ENV LAUNCH_JBOSS_IN_BACKGROUND true

# USER jboss

# Expose the ports we're interested in
EXPOSE 8080 9990

RUN $JBOSS_HOME/bin/add-user.sh admin admin --silent

# Set the default command to run on boot
# This will boot WildFly in the standalone mode and bind to all interface
ENTRYPOINT ["/opt/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]
CMD ["--server-config=standalone.xml"]