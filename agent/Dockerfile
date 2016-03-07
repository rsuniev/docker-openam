# Centos based container with Java and Tomcat
FROM tomcat:8-jre8
MAINTAINER rsuniev

ENV OPENAM_AGENT_HOME /opt/openam-policy-agent

ADD ./files/Tomcat-v6-Agent_3.5.0.zip .

RUN unzip Tomcat-v6-Agent_3.5.0.zip
RUN mkdir -p ${OPENAM_AGENT_HOME}
RUN mv j2ee_agents/tomcat_v6_agent/* ${OPENAM_AGENT_HOME}
RUN rm -rf Tomcat-v6-Agent_3.5.0.zip

ADD ./files/pwd.txt /tmp
ADD ./files/install-properties.txt ${OPENAM_AGENT_HOME}   

RUN ${OPENAM_AGENT_HOME}/bin/agentadmin --acceptLicense --install --useResponse ${OPENAM_AGENT_HOME}/install-properties.txt

EXPOSE 8080

CMD ["catalina.sh", "run"]
