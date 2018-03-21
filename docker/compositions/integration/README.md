# FUI StoreConnect's Sensors API Docker composition - Integration deployment environment

This repository contains the definition of the [Docker composition](https://docs.docker.com/compose/overview/) for the FUI [StoreConnect](https://www.pole-scs.org/projet/storeconnect) project's Sensors API in its integration deployment environment.

## Directory layout

This directory is organized as follows:

File/Directory                              | Description
------------------------------------------- | -----------------------------------------------------------------------------------------------------------
[docker-compose.yml](./docker-compose.yml)  | The Docker composition file of the integration deployment environment of the FUI StoreConnect's Sensors API
[conf/](./conf)                             | Related configuration files to the Docker composition

## Prerequisites

- The FUI StoreConnect's Sensors API specification
    - follows the [OGC SensorThings API specification](https://github.com/opengeospatial/sensorthings). Thereby, a good understanding of the OGC SensorThings API specification is required before to use the FUI StoreConnect Sensors API.
- The FUI StoreConnect's Sensors API implementation
    - is based on the [FraunhoferIOSB's GOC SensorThings implementation server](https://github.com/FraunhoferIOSB/FROST-Server). Here too, a good understanding of this implementation is required to use a FUI StoreConnect's Sensors API instance.
    - can be easily deployed via [Docker](https://docs.docker.com/) and more precisely a [Docker composition](https://docs.docker.com/compose/overview/). Here again, you should be familiar with the Docker ecosystem to easily install/deploy this FUI StoreConnect's Sensors API instance. 

## How to...

### ... access to the official integration deployment environment instance of the FUI StoreConnect's Sensors API?

The official FUI StoreConnect's Sensors AP's integration deployment environment instance can be reached [here](http://apicapteur.westeurope.cloudapp.azure.com:8080/SensorThingsService/v1.0).

### ... deploy its own FUI StoreConnect's Sensors API's integration deployment environment instance?

This FUI StoreConnect's Sensors API instance can be easily deployed via [Docker](https://docs.docker.com/) and more precisely a [Docker composition](https://docs.docker.com/compose/overview/).
Once `docker` and `docker-compose` is correctly installed to your host, then simply execute:

```bash
    docker-compose up
```

Once Docker composition is started, then the FUI StoreConnect's Sensors API instance can be reached by browsing to

```
    <docker_host>:8080/SensorThingsService/v1.0
```

Where `<docker_host>` is the Docker host (typically `localhost` in case of a Docker native installation).

#### In case of first time execution

When the composition is ran for the first time, the FUI StoreConnect's Sensors API's database starts an initialization process, causing the FUI StoreConnect's Sensors API's server not to be available. In addition, a second database initialization process has to be manually done to have a fully initialized environment.

The following step-by-step guide helps you to have a FUI StoreConnect's Sensor API instance fully operational if ran for the first time:

1. Only start the FUI StoreConnect's Sensor API database service by executing:
    ```bash
        docker-compose up --force-recreate storeconnect-sensors-api-database
    ```
2. Wait until database is ready to accept connection (see associated `storeconnect-sensors-api-database`'s log messages)
3. Start the whole composition by executing:
    ```bash
        docker-compose up
    ```    
4. Wait until web service is ready to accept connect (see associated `storeconnect-sensors-api-server`'s log messages)
5. Manually trigger the second database initialization process by:
    1. Browsing to `<docker_host>:8080/SensorThingsService/DatabaseStatus`, where `<docker_host>` is your Docker host (typically `localhost` in case of native Docker installation)
    2. Start the second database initialization process by clicking on the `Do Update` button
    
Then now you have a fully operational FUI StoreConnect's Sensor API instance.
