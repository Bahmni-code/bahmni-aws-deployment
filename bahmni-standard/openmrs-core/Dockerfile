FROM tomcat:7-jdk8-adoptopenjdk-hotspot

RUN apt update && apt install -y mysql-client gettext coreutils curl wget openssl
ARG WAR_FILE
COPY ${WAR_FILE} /usr/local/tomcat/webapps/openmrs.war
#RUN wget -O /usr/local/tomcat/webapps/openmrs.war ${WAR_FILE}

#ARG SETENV
RUN curl -o /usr/local/tomcat/bin/setenv.sh https://github.com/Bahmni-code/bahmni-aws-deployment/bahmni-standard/openmrs-core/setenv.sh
#COPY ${SETENV} /usr/local/tomcat/bin/setenv.sh
RUN curl -o /usr/local/tomcat/bin/wait-for-it.sh https://github.com/Bahmni-code/bahmni-aws-deployment/bahmni-standard/openmrs-core/wait-for-it.sh
RUN curl -o /usr/local/tomcat/bin/startup.sh https://github.com/Bahmni-code/bahmni-aws-deployment/bahmni-standard/openmrs-core/startup.sh


#COPY wait-for-it.sh /usr/local/tomcat/wait-for-it.sh
#COPY startup.sh /usr/local/tomcat/startup.sh

RUN sed -i '/Connector port="8080"/a URIEncoding="UTF-8" relaxedPathChars="[]|" relaxedQueryChars="[]|{}^&#x5c;&#x60;&quot;&lt;&gt;"' /usr/local/tomcat/conf/server.xml

RUN locale-gen

RUN chmod +x /usr/local/tomcat/bin/wait-for-it.sh
RUN chmod +x /usr/local/tomcat/bin/startup.sh

#CMD ["/bin/bash","/usr/local/tomcat/bin/startup.sh"]
CMD ["sh", "/usr/local/tomcat/bin/startup.sh"]