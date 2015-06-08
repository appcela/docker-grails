FROM	appcela/docker-debian-oracle-jdk:latest

# Install Grails
ENV GRAILS_VERSION 2.4.5

WORKDIR /usr/lib/jvm

RUN apt-get update && apt-get install unzip && \
    curl -SLO http://dist.springframework.org.s3.amazonaws.com/release/GRAILS/grails-$GRAILS_VERSION.zip
RUN unzip grails-$GRAILS_VERSION.zip && \
    ln -s grails-$GRAILS_VERSION grails && \
    apt-get autoclean && apt-get --purge -y autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Setup Grails path.
ENV GRAILS_HOME /usr/lib/jvm/grails
ENV PATH $GRAILS_HOME/bin:$PATH

# Create App Directory
WORKDIR /
RUN mkdir /app
WORKDIR /app
VOLUME ["/app"]

# Expose Ports (web=8080, debug=5005)
EXPOSE 5005 8080

# Create dependency cache settings and download the initial dependencies
COPY settings.groovy /root/.grails/settings.groovy
RUN grails help
