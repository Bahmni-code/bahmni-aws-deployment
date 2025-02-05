# Use Tomcat 7 with JDK 8 from AdoptOpenJDK
FROM tomcat:7-jdk8-adoptopenjdk-hotspot

# Update package list and install required tools
RUN apt update && apt install -y mysql-client gettext coreutils curl wget openssl locales \
    && locale-gen en_US.UTF-8

# Set argument for WAR file
ARG WAR_FILE

# Copy WAR file from local build context
COPY ${WAR_FILE} /usr/local/tomcat/webapps/openmrs.war

# Download configuration scripts
RUN curl -o /usr/local/tomcat/bin/setenv.sh https://github.com/Bahmni-code/bahmni-aws-deployment/bahmni-standard/openmrs-core/setenv.sh \
    && curl -o /usr/local/tomcat/bin/wait-for-it.sh https://github.com/Bahmni-code/bahmni-aws-deployment/bahmni-standard/openmrs-core/wait-for-it.sh \
    && curl -o /usr/local/tomcat/bin/startup.sh https://github.com/Bahmni-code/bahmni-aws-deployment/bahmni-standard/openmrs-core/startup.sh

# Ensure scripts have execution permissions
RUN chmod +x /usr/local/tomcat/bin/wait-for-it.sh \
    && chmod +x /usr/local/tomcat/bin/startup.sh \
    && chmod +x /usr/local/tomcat/bin/setenv.sh

# Improve Tomcat's URI encoding settings for compatibility
RUN sed -i '/Connector port="8080"/a URIEncoding="UTF-8" relaxedPathChars="[]|" relaxedQueryChars="[]|{}^&#x5c;&#x60;&quot;&lt;&gt;"' /usr/local/tomcat/conf/server.xml

# Set the working directory to Tomcat
WORKDIR /usr/local/tomcat

# Expose Tomcat port
EXPOSE 8080

# Start Tomcat properly
CMD ["catalina.sh", "run"]
