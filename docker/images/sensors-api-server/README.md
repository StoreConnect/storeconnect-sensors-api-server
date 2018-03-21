# FUI StoreConnect's Sensors API's server Docker image

Docker image of the FUI [StoreConnect](https://www.pole-scs.org/projet/storeconnect)'s Sensor API's server part.

This image is based on the [FraunhoferIOSB's FROST-Server image](https://hub.docker.com/r/fraunhoferiosb/frost-server/). 
    
## Tags

Tag                         | Description
--------------------------- | ----------------------------------------------------------------------------------------------------------------
[latest](./1.0-1.4)         | Copy of the [1.0-1.5.2](./1.0-1.5.2) version
[1.0-1.5.2](./1.0-1.5.2)    | `1.0` version, linked to the `1.5.2` FraunhoferIOSB's FROST-Server image

## How to...

### ... use this image?

This image is hardly dependent on a database layer. Prefer use [associated Docker composition files](../../compositions) to run a full FUI StoreConnect's Sensors API stack.

### ... build this image? 

```
    docker build -t storeconnect/sensors-api-server:<tag> .
```

Where `<tag>` is the desired tag. 