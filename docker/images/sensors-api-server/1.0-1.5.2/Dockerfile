FROM fraunhoferiosb/frost-server:1.5.2

# Extract WAR to be able to personalize its configuration
RUN unzip -d /usr/local/tomcat/webapps/SensorThingsService /usr/local/tomcat/webapps/FROST-Server.war && \
    rm /usr/local/tomcat/webapps/FROST-Server.war