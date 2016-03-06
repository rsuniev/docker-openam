FROM java:8

MAINTAINER rustem.suniev@gmail.com

WORKDIR /opt

ADD ./files/OpenDJ-2.6.3.zip ./staging/

RUN unzip staging/OpenDJ-2.6.3.zip -d /opt/ && rm -fr /opt/staging

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/

RUN echo "/opt/opendj/instances/template" > /opt/opendj/instance.loc  && \
    mkdir -p /opt/opendj/instances/template/lib/extensions

# Note - for some reason the entire command must be quoted or DJ launches the GUI
RUN /opt/opendj/setup --cli -p 389 --ldapsPort 636 --adminConnectorPort 4444 --rootUserDN cn=diradmin --enableStartTLS --generateSelfSignedCertificate  --sampleData 5 --baseDN "dc=example,dc=com" -h localhost --rootUserPassword password --acceptLicense --no-prompt --doNotStart

EXPOSE 389 636 4444 8080

ADD run.sh /opt/opendj/run.sh

# Copy in the template the first time DJ runs, and start DJ

CMD ["/opt/opendj/run.sh"]

