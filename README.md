# FUI StoreConnect's Sensors API

This repository contains the sources and documentation of the FUI [StoreConnect](https://www.pole-scs.org/projet/storeconnect) project's Sensors API part.

## Authors

[Aurélien Bourdon](https://github.com/abourdon), [Romain Rouvoy](http://romain.rouvoy.fr), [Lionel Seinturier](http://www.lifl.fr/~seinturi).

## Directory layout

This directory is organized as follows:

Directory                                   | Description
------------------------------------------- | --------------------------------------------------------
[docker](./docker)                          | Docker files of the FUI StoreConnect's Sensors API
[third-parties](./third-parties)            | Third parties used by the FUI StoreConnect's Sensors API 

## Prerequisites

- The FUI StoreConnect's Sensors API specification follows the [OGC SensorThings API specification](https://github.com/opengeospatial/sensorthings). Thereby, a good understanding of the OGC SensorThings API specification is required before to use the FUI StoreConnect Sensors API.
- The FUI StoreConnect's Sensors API implementation is based on the [FraunhoferIOSB's GOC SensorThings implementation server](https://github.com/FraunhoferIOSB/SensorThingsServer). Here too, a good understanding of this implementation is required to use a FUI StoreConnect's Sensors API instance. 

## How to...

### ... access to the official FUI StoreConnect's Sensors API instances?

The table bellow lists the set of FUI StoreConnect's Sensors API instances and their associated access links.

Instance name   | Description                           | Access link
--------------- | ------------------------------------- | ---------------------
integration     | Integration deployment environment    | https://goo.gl/i3gGBQ

### ... clone sources?

This project uses [Git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules), then beware to clone this project by using the `--recurse-submodules` option:

```bash
    git clone --recurse-submodules https://github.com/StoreConnect/storeconnect-sensors-api.git
```

## Note

Currently, the FUI StoreConnect's Sensor API exactly follows the OGC SensorThings API. This way, there is no pre-defined types related to the FUI StoreConnect ecosystem nor restriction about the use of OGC SensorThings API (e.g., a `FeatureOfInterest` would only be a `Store` when using the FUI StoreConnect API).
Thus, a next step would be to extend the OGC SensorThings's API to create FUI StoreConnect related types to then restrict the use of the FUI StoreConnect's Sensors API to only types of the FUI StoreConnect ecosystem.

## How to contribute

Wants to contribute? Feel free to make a `pull request` following the [contributing](./CONTRIBUTING.md) instructions.