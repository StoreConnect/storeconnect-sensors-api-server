# FUI StoreConnect's OGC SensorThings API's server Docker image

Unofficial Docker image of the [FraunhoferIOSB's SensorThingsServer](https://github.com/FraunhoferIOSB/SensorThingsServer), main implementation of the [OGC SensorThings API](https://github.com/opengeospatial/sensorthings).

## Presentation

As explained [here](https://github.com/FraunhoferIOSB/SensorThingsServer/issues/38), the associated FraunhoferIOSB's SensorThingsServer Docker image is not available in an official Docker repository.
However, as the FUI StoreConnect Sensors API server is based on the FraunhoferIOSB's SensorThingsServer, the FUI StoreConnect project currently hosts an exact copy of the FraunhoferIOSB's SensorThingsServer Docker image.

Thus, this copy of the FraunhoferIOSB's SensorThingsServer Docker image is located in the [FUI StoreConnect's Docker repository](https://hub.docker.com/r/storeconnect/sensorthings-server/) and can be reached by pulling: 

    storeconnect/sensorthings-server:<tag>
    
Where `<tag>` is the desired tag.
    
## Tags

The following table described all available tags.

Tag     | Description
------- | ------------------------------------------------------------------------------------------------------------------------
latest  | The latest version (at the moment based on the latest commit we know, as there is not yet an available released version)

## Create a FUI StoreConnect's OGC SensorThings API's server Docker image

As said, the FUI StoreConnect's OGC SensorThings API's server Docker image is an exact copy of the FraunhoferIOSB's SensorThingsServer's one. This way, create a new FUI StoreConnect's OGC SensorThings API's server Docker image can be done as follows:

1. Go to the [third-parties](../../../third-parties) directory
2. Execute
    ```bash
        mvn clean package -f ensorthings-server/pom.xml
    ```
    Then a new FraunhoferIOSB's OGC SensorThingsServer Docker image is building and 2 tags are generated: the current version and `latest` (a copy of the former).
3. Now create the FUI StoreConnect's OGC SensorThings API's server Docker image by executing:
    ```
        docker tag sensorthings-server:latest storeconnect/sensorthings-server:latest
    ```

## Additional notes

This image will be deleted as soon as the FraunhoferIOSB's SensorThingsServer will be hosted in an official Docker repository, i.e., when [the associated issue](https://github.com/FraunhoferIOSB/SensorThingsServer/issues/38) will be resolved. 