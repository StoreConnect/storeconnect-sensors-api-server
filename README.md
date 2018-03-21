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

- The FUI StoreConnect's Sensors API specification follows the [OGC SensorThings API specification](https://github.com/opengeospatial/sensorthings);
- The FUI StoreConnect's Sensors API specification uses the [GeoJSON format](http://geojson.org/) to encode geographic data;
- The FUI StoreConnect's Sensors API implementation is based on the [FraunhoferIOSB's GOC SensorThings implementation server](https://github.com/FraunhoferIOSB/FROST-Server). 

## The StoreConnect's Sensor API data model

The StoreConnect’s Sensor API data model follows the [OGC SensorThings API data model](http://docs.opengeospatial.org/is/15-078r6/15-078r6.html) which is summarized by the following picture:

![OGC SensorThings API data model](http://ogc-iot.github.io/ogc-iot-api/img/SensorThingsUML_Core.svg)

However, the OGC SensorThings API defines a generic model, that can be specified according to the specific use case.

The following section defines the OGC SensorThings API’s data specification when using it within the StoreConnect context. Each following major sections concerns a specific OGC SensorThings API data model type which has been extended by the StoreConnect Sensor API data model.

### `Datastream`

Any StoreConnect Sensor API's OGC SensorThings' `Datastream` uses an `OM_Observation` as a `observationType` attribute. This way, the content of result has to be specified, as explained in the next section.

### `Observation#result`

According to the [main StoreConnect's ontology](https://github.com/StoreConnect/storeconnect-ontologies-api/tree/develop/ontologies/storeconnect-main), any StoreConnect's `sosa:Sensor` produces a `sosa:Observation` linked to a `sosa:Result` which is a `sc:MotionEvent` (`sosa` for the [OGC W3C SOSA ontology](https://www.w3.org/TR/vocab-ssn/) namespace, `sc` for the [StoreConnect ontology](https://github.com/StoreConnect/storeconnect-ontologies-api/tree/develop/ontologies/storeconnect-main) namespace).
This way, any OGC SensorThings' `Observation` can be seen as a `sosa:Observation` and any OGC SensorThings' `Observation#result` as a `sc:MotionEvent`.

In the StoreConnect's Sensor API, a `sc:MotionEvent` is represented as a `MotionEvent` with the following attributes:

Attribute Name  | Attribute Type        | Attribute Description
--------------- | --------------------- | --------------------------------------------------------------------------------
`subject`       | `MotionSubject`       | Identification of the phenomenon (identifier and physical characteristics)
`location`      | `VenueLocation`       | The location of this motion event, i.e., where the phenomenon has been perceived
`speed`         | `Speed`               | (Optional) Recorded speed of the perceived phenomenon
`orientation`   | `Orientation`         | (Optional) Orientation of the perceived phenomenon
`state`         | `MotionState`         | (Optional) Motion state of the perceived phenomenon

#### `MotionSubject`

As for the `sc:MotionSubject` in the StoreConnect's ontology, a `MotionSubject` describes identification information about the perceived phenomenon. It consists of two parts:
- An identifier
- Physical or behavioral trait characteristics

An identifier is always relative to the associated `Sensor` from which the `Observation` has been made

_Note: For the moment, there is no defined physical or behavioral trait characteristics (coming in a future StoreConnect's Sensor API version). This value can so be omitted, and then, a `MotionEventSubject` is only pointing to a given identifier, relatively unique from the associated Sensor._ 

#### `VenueLocation`

Any OGC SensorThings' `Thing` has a location, as well as a StoreConnect Sensor API's `MotionEvent`. In the StoreConnect Sensor API's context, a location is typed as a `VenueLocation` (`sc:Location` inside the StoreConnect's ontology). Description of this type is given by the following table:

_Note: The term `VenueLocation` has been chosen instead of simply `Location` because the OGC SensorThings API already defines the `Location` type._ 

Attribute Name  | Attribute Type                        | Attribute Description
--------------- | ------------------------------------- | ----------------------------------------------------------------------------------
`coordinates`   | `GeoJSON Point`                       | The coordinates of this event, relatively to the associated `venue`
`venue`         | `Venue`                               | Link to the associated venue where the phenomenon has been perceived
`accuracy`      | `float` (percentage from 0.0 to 1.0)  | (Optional) The accuracy, or confidence, to taking into account when reading values

##### `Venue`

Details about the venue associated to where (location) the `MotionEvent` has been perceived. `Venue`'s attributes are described bellow:

Attribute Name  | Attribute Type    | Attribute Description
--------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------
`building`      | `int`             | The building number where the venue comes from
`floor`         | `int`             | The building's floor number where the venue comes from
`zone`          | `GeoJSON Polygon` | (Optional) The building floor's zone where the venue comes from. Typically described as a polygon in a 2D representation

#### `Speed`

Defines the recorded speed of the perceived phenomenon. Attributes are given in the following table:

Attribute Name  | Attribute Type                        | Attribute Description
--------------- | ------------------------------------- | --------------------------------------------------------------------------------------
`value`         | `float` (m/s)                         | The recorded speed of the perceived phenomenon
`accuracy`      | `float` (percentage from 0.0 to 1.0)  | (Optional) The accuracy, or confidence, to taking into account when reading the `value`

#### `Orientation`

Defines the orientation of the perceived phenomenon. Attributes are given in the following table:

Attribute Name  | Attribute Type                        | Attribute Description
--------------- | ------------------------------------- | --------------------------------------------------------------------------------------
`value`         | `float` (degrees)                     | The orientation of the perceived phenomenon
`accuracy`      | `float` (percentage from 0.0 to 1.0)  | (Optional) The accuracy, or confidence, to taking into account when reading the `value`

#### `MotionState`

As for the `sc:MotionState`, a `MotionState` describes the actual moving state of the perceived phenomenon. It can be either `Walking` or `Stopping` associated to an accuracy value:

Attribute Name  | Attribute Type                                | Attribute Description
--------------- | --------------------------------------------- | --------------------------------------------------------------------------------------
`value`         | `CharacterString` (`Walking` or `Stopping`)   | Actual moving state of the perceived phenomenon
`accuracy`      | `float` (percentage from 0.0 to 1.0)          | (Optional) The accuracy, or confidence, to taking into account when reading the `value`

### `Location`

#### `Location#location`

As described above, a OGC SensorThings' `Location#location` is a StoreConnect Sensor API's `VenueLocation`.

#### `Location#encodingType`

As there is no yet existing encoding type for the `Location#encodingType` from the OGC SensorThings API, the StoreConnect Sensor API simply ignores it. In addition, as defined above, only a `VenueLocation` can be affected to the `Location#location` attribute.   

### `ObservedProperty`

The main StoreConnect preoccupation is the ability to observe _motions_ within given _venues_ (`Venue`). Hence, the only `ObservedProperty` is the notion of `Motion`. This way, we say that a `Motion` is a specific type of `ObservedProperty`. 

### `FeatureOfInterest`

#### `FeatureOfInterest#feature`

Here again, as the main StoreConnect preoccupation is the ability to observe _motions_ (`Motion`) within given _venues_ (`Venue`), the `FeatureOfInterest#feature` must represent a known `Venue`.

#### `FeatureOfInterest#encodingType` 

As there is no yet existing encoding type for the `FeatureOfInterest#encodingType` from the OGC SensorThings API, the StoreConnect Sensor API simply ignores it. In addition, as defined above, only a `Venue` can be affected to the `FeatureOfInterest#feature` attribute.

### `Sensor#metadata`

For the moment, there is no restriction to the definition of how a StoreConnect's `Sensor` can be defined. Hence, the StoreConnect's `Sensor#metadata` type follows the OGC SensorThings API specification and can either be a PDF or a [SensorML](http://www.opengis.net/doc/IS/SensorML/2.0) document. 

### Final overview of StoreConnect's extension of the OGC SensorThings API data model

The following picture summarizes the added extensions by the StoreConnect Sensor API data model (in red) to the OGC SensorThings API data model (in white).

![StoreConnect Sensor API data model (based on the OGC SensorThings API data model)](resources/storeconnect-sensor-api-data-model.svg)

_Note: this picture has been generated via [Draw.io](https//www.draw.io). Any modification can be applied by importing its associated [raw file](resources/storeconnect-sensor-api-data-model.xml)._

## How to...

### ... insert a sensor's observation into the StoreConnect's Sensor API?

**To be described**

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

## Additional note

For the moment, there is no additional check for incoming data. Indeed, the StoreConnect Sensor API implementation is a copy of the FraunhoferIOSB's GOC SensorThings implementation. Thus, there is no type control over extended types brought by the StoreConnect Sensor API model.

## How to contribute

Wants to contribute? Feel free to make a `pull request` following the [contributing](./CONTRIBUTING.md) instructions.