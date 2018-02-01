# FUI StoreConnect's Sensors API

This repository contains the sources and documentation of the FUI [StoreConnect](https://www.pole-scs.org/projet/storeconnect) project's Sensors API part.

## Authors

[Aurélien Bourdon](https://github.com/abourdon), [Romain Rouvoy](http://romain.rouvoy.fr), [Lionel Seinturier](http://www.lifl.fr/~seinturi).

## Directory layout

This repository is organized as follows:

Directory                                   | Description
------------------------------------------- | --------------------------------------------------------
[sources](./sources)                        | Sources of the StoreConnect's Sensors API
[docker-compose.yml](./docker-compose.yml)  | The Docker composition of the StoreConnect's Sensors API

## Prerequisites

- The FUI StoreConnect's Sensors API specification
    - follows the [OGC SensorThings API specification](https://github.com/opengeospatial/sensorthings). Thereby, a good understanding of the OGC SensorThings API specification is required before to use the FUI StoreConnect Sensors API.
- The FUI StoreConnect's Sensors API implementation
    - is based on the [FraunhoferIOSB's GOC SensorThings implementation server](https://github.com/FraunhoferIOSB/SensorThingsServer). Here too, a good understanding of this implementation is required to use a FUI StoreConnect's Sensors API instance.
    - can be easily deployed via [Docker](https://docs.docker.com/) and more precisely a [Docker composition](https://docs.docker.com/compose/overview/). Here again, you should be familiar with the Docker ecosystem to easily install/deploy a FUI StoreConnect's Sensors API instance. 

## How to...

### ... access to the official FUI StoreConnect's Sensors API instance?

The official FUI StoreConnect's Sensors API instance can be reached [here](http://apicapteur.westeurope.cloudapp.azure.com:8080/SensorThingsService/v1.0).

### ... deploy its own FUI StoreConnect's Sensors API instance?

The FUI StoreConnect's Sensors API instance can be easily deployed via [Docker](https://docs.docker.com/) and more precisely a [Docker composition](https://docs.docker.com/compose/overview/).
Once `docker` and `docker-compose` is correctly installed to your host, then deploy its own FUI StoreConnect's Sensors API instance can be simply done by executing the following command line from this directory:

```bash
    docker-compose up
```

Once Docker composition is started, then the FUI StoreConnect's Sensors API instance can be reached by browsing to

```
    <docker_host>:8080/SensorThingsService/v1.0
```

#### First time execution

When the composition is ran for the first time, the FUI StoreConnect's Sensors API's database starts an initialization process, causing the FUI StoreConnect's Sensors API's web service not to be available. In addition, a second database initialization process has to be manually done to have a fully initialized environment.

The following step-by-step guide helps you to have a FUI StoreConnect's Sensor API instance fully operational if ran for the first time:

1. Only start the FUI StoreConnect's Sensor API database service by executing:
    ```bash
        docker-compose up --force-recreate storeconnect-sensorthings-database
    ```
2. Wait until database is ready to accept connection (see associated `storeconnect-sensorthings-database`'s log messages)
3. Start the whole composition by executing:
    ```bash
        docker-compose up
    ```    
4. Wait until web service is ready to accept connect (see associated `storeconnect-sensorthings-server`'s log messages)
5. Manually trigger the second database initialization process by:
    1. Browsing to `<docker_host>:8080/SensorThingsService/DatabaseStatus`, where `<docker_host>` is your Docker host (`localhost` by default if using a native Docker installation)
    2. Start the second database initialization process by clicking on the `Do Update` button
    
Then now you have a fully operational FUI StoreConnect's Sensor API instance.

### ... create its own FUI StoreConnect's Sensor API Docker image?

The FUI StoreConnect's Sensors API Docker image is based on the [FraunhoferIOSB's OGC SensorThings](https://github.com/FraunhoferIOSB/SensorThingsServer)'s one. That's it, building the The FUI StoreConnect's Sensors API Docker image can be done by executing:

```bash
    mvn clean package -f sources/ensorthings-server/pom.xml 
```

Then a new FraunhoferIOSB's OGC SensorThingsServer Docker image is building and 2 tags are generated: the current version and `latest` (a copy of the former).

Now, to create a new FUI StoreConnect's Sensor API Docker image, simply create a new tag linked to any of the 2 formers. For instance:

```
    docker tag <FraunhoferIOSB OGC SensorThingsServer image name>:latest <your Docker registry/repository>/storeconnect-sensorthings:latest
``` 

Now you can re-up your composition by executing:

```bash
    docker-compose up --force-recreate
```    

## Note

From now, the FUI StoreConnect's Sensor API exactly follows the OGC SensorThings API. This way, there is no pre-defined types related to the FUI StoreConnect ecosystem nor restriction about use of OGC SensorThings API (e.g., a `FeatureOfInterest` could only be a `Store` when using the FUI StoreConnect API).
Thus, a next step would be to extend the OGC SensorThings's API to create FUI StoreConnect related types to then restrict the use of the FUI StoreConnect's Sensors API to only types of the FUI StoreConnect ecosystem.

## How to contribute

Wants to contribute? Feel free to make a `pull request` following the [contributing](./CONTRIBUTING.md) instructions.