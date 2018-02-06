# FUI StoreConnect's Sensors API's database Docker image, on a PostGIS database

Docker image of the FUI [StoreConnect](https://www.pole-scs.org/projet/storeconnect)'s Sensor API's database part, based on a [PostGIS database](https://postgis.net/).

This image is based on the [PostGIS Docker image](https://github.com/appropriate/docker-postgis). 
    
## Tags

Tags follow the same [FUI StoreConnect's SensorThingsServer Docker image](https://hub.docker.com/r/storeconnect/sensorthings-server/)'s tags.

Tag                 | Description
------------------- | ---------------------------------------------------------------
[latest](./1.0-10)  | Copy of the [1.0-10](./1.0-10) version
[1.0-10](./1.0-10)  | `1.0` version, linked to the `1.0` PostGIS Docker image version

## How to...

### ... use this image?

There is no reason to run this image without a server layer. Prefer use [associated Docker composition files](../../compositions) to run a full FUI StoreConnect's Sensors API stack.

### ... build this image? 

```
    docker build -t storeconnect/sensors-api-postgis-database:<tag> .
```

Where `<tag>` is the desired tag. 