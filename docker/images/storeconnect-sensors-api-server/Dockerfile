# Use the docker.io/storeconnect/sensorthings-server:latest because official FraunhoferIOSB SensorThingsServer's Docker image is not yet available
# See https://github.com/FraunhoferIOSB/SensorThingsServer/issues/38 for more detais
FROM storeconnect/sensorthings-server:latest

# Extract WAR to be able to personalize its configuration
RUN unzip -d /usr/local/tomcat/webapps/SensorThingsService /usr/local/tomcat/webapps/SensorThingsService.war && \
    rm /usr/local/tomcat/webapps/SensorThingsService.war