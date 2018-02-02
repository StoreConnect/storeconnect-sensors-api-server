# FUI StoreConnect's Sensors API's server Docker image

Docker image of the FUI [StoreConnect](https://www.pole-scs.org/projet/storeconnect)'s Sensor API's server part.

This image is based on the [FUI StoreConnect's SensorThingsServer Docker image](https://hub.docker.com/r/storeconnect/sensorthings-server/) by adding a way to configure the copied WAR file. 
    
## Tags

Tags follow the same [FUI StoreConnect's SensorThingsServer Docker image](https://hub.docker.com/r/storeconnect/sensorthings-server/)'s tags.

Tag     | Description
------- | ------------------------------------------------------------------------------------------------------------------------
latest  | The latest version (at the moment based on the latest commit we know, as there is not yet an available released version)

## How to...

### ... use this image?

This image is hardly dependent on a database layer. Prefer use [associated Docker composition files](../../compositions) to run a full FUI StoreConnect's Sensors API stack.

### ... build this image? 

```
    docker build -t storeconnect/storeconnect-sensors-api-server:<tag> .
```

Where `<tag>` is the desired tag. 