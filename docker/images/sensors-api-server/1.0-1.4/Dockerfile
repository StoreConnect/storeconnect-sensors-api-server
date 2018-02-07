FROM fraunhoferiosb/sensorthingsserver:1.4

# Extract WAR to be able to personalize its configuration
RUN unzip -d /usr/local/tomcat/webapps/SensorThingsService /usr/local/tomcat/webapps/SensorThingsService.war && \
    rm /usr/local/tomcat/webapps/SensorThingsService.war