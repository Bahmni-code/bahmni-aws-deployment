# Step 1: Use the official Tomcat image as a base
FROM tomcat:9.0-jdk11-openjdk

# Step 2: Set environment variables for AWS RDS
ENV DB_HOST=openmrs.cdc6cy0k0jft.ap-south-1.rds.amazonaws.com
ENV DB_PORT=3306
ENV DB_NAME=openmrs
ENV DB_USER=admin
ENV DB_PASSWORD=Qawsedrf2025

# Step 3: Copy the OpenMRS WAR file to the Tomcat webapps directory
ARG WAR_FILE
COPY ${WAR_FILE} /usr/local/tomcat/webapps/ROOT.war

# Step 4: Expose the Tomcat HTTP port
EXPOSE 8080

# Step 5: Start Tomcat when the container runs
CMD ["catalina.sh", "run"]
