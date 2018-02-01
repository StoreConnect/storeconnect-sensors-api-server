# FUI StoreConnect's Sensors API sources

This repository contains the sources of the FUI [StoreConnect](https://www.pole-scs.org/projet/storeconnect) project's Sensors API part.

## Directory layout

This repository is organized as follows:

File/Directory                                  | Description
----------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------
[sensorthings-server](./sensorthings-server)    | A fork of the [FraunhoferIOSB's OGC SensorThings implementation server](https://github.com/FraunhoferIOSB/SensorThingsServer) 
    
## Note

From now, the FUI StoreConnect's Sensor API exactly follows the OGC SensorThings API. This way, there is no pre-defined types related to the FUI StoreConnect ecosystem nor restriction about use of OGC SensorThings API (e.g., a `FeatureOfInterest` could only be a `Store` when using the FUI StoreConnect API).
Thus, a next step would be to extend the OGC SensorThings's API to create FUI StoreConnect related types to then restrict the use of the FUI StoreConnect's Sensors API to only types of the FUI StoreConnect ecosystem. 
