# Purpose

This specification is intended to define a standardized way of communicating with lighting systems for real-time monitoring and control and to allow data collection between control systems and / or peripheral devices.

**NOTE:** need to add API to query last-known update...identify what was done and when (and by whom?)

# Scope

The scope of this document is limited to providing a payload structure and endpoint type definitions to allow basic control and data acquisition. The addition of product specific features is left to the implementer, but to be in compliance the product must support the basic set of features specified below.

# Definitions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

# Endpoints
## Sensors
### Talking to one sensor
```
GET http://[domain:port]/agroapi/[version]/lights/sensors/[sensorid]/info  
```
Returns [Info](general.md#info-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/sensors/[sensorid]/version  
```
Returns [Version](general.md#version-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/sensors/[sensorid]/location  
```
Returns [Location](general.md#location-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/sensors/[sensorid]/ppf  
```
Returns [Light PPF](https://github.com/open-ag-tech/api-spec/blob/master/versions/light-0.0.1.md#light-ppf)  

```
GET http://[domain:port]/agroapi/[version]/lights/sensors/[sensorid]/ppfd  
```
Returns [Light PPFD](https://github.com/open-ag-tech/api-spec/blob/master/versions/light-0.0.1.md#light-ppfd)  

### Talking to all sensors
```
GET http://[domain:port]/agroapi/[version]/lights/sensors/info  
```
Returns an array of [Info](general.md#info-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/sensors/version  
```
Returns an array of [Version](general.md#version-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/sensors/location  
```
Returns an array of [Location](general.md#location-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/sensors/ppf  
```
Returns an array of [Light PPF](https://github.com/open-ag-tech/api-spec/blob/master/versions/light-0.0.1.md#light-ppf)  

```
GET http://[domain:port]/agroapi/[version]/lights/sensors/ppfd  
```
Returns an array of [Light PPFD](https://github.com/open-ag-tech/api-spec/blob/master/versions/light-0.0.1.md#light-ppfd)  

### Talking to all sensors in a zone
```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/sensors/info  
```
Returns an array of [Info](general.md#info-data)  

```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/sensors/version  
```
Returns an array of [Version](general.md#version-data)  

```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/sensors/location  
```
Returns an array of [Location](general.md#location-data)  

```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/sensors/ppf  
```
Returns an array of [Light PPF](https://github.com/open-ag-tech/api-spec/blob/master/versions/light-0.0.1.md#light-ppf)  

```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/sensors/ppfd  
```
Returns an array of [Light PPFD](https://github.com/open-ag-tech/api-spec/blob/master/versions/light-0.0.1.md#light-ppfd)  

### Light PPF
| Name      | Description                      | Unit     |
| --------- | -------------------------------- | -------- |
| id        | Unique id of the device          | uid      |
| timestamp | UTC timestamp of the measurement | datetime |
| red       | Level of red spectrum light      | PPF      |
| blue      | Level of blue spectrum light     | PPF      |
| green     | Level of green spectrum light    | PPF      |
| uv        | Level of ultraviolet light       | PPF      |
| infrared  | Level of infrared light          | PPF      |
| par       | Level of absorbable light        | PPF      |
| light     | Level of all spectrums of light  | PPF      |

### Light PPFD
| Name      | Description                      | Unit     |
| --------- | -------------------------------- | -------- |
| id        | Unique id of the device          | uid      |
| timestamp | UTC timestamp of the measurement | datetime |
| red       | Level of red spectrum light      | PPFD     |
| blue      | Level of blue spectrum light     | PPFD     |
| green     | Level of green spectrum light    | PPFD     |
| uv        | Level of ultraviolet light       | PPFD     |
| infrared  | Level of infrared light          | PPFD     |
| par       | Level of absorbable light        | PPFD     |
| light     | Level of all spectrums of light  | PPFD     |

## Fixtures
### Talking to one fixture
```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/[fixtureid]/info
```
Returns [Info](general.md#info-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/[fixtureid]/version  
```
Returns [Version](general.md#version-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/[fixtureid]/location
```
Returns [Location](general.md#location-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/[fixtureid]/config
```
Returns [Fixture Configuration](https://github.com/open-ag-tech/api-spec/blob/master/versions/light-0.0.1.md#fixture-configuration)  

```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/[fixtureid]/power
```
Returns [Fixture Power](https://github.com/open-ag-tech/api-spec/blob/master/versions/light-0.0.1.md#fixture-power)  

### Talking to all fixtures
```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/info
```
Returns an array of [Info](general.md#info-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/version  
```
Returns an array of [Version](general.md#version-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/location
```
Returns an array of [Location](general.md#location-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/config
```
Returns an array of [Fixture Configuration](https://github.com/open-ag-tech/api-spec/blob/master/versions/light-0.0.1.md#fixture-configuration)  

```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/power
```
Returns an array of [Fixture Power](https://github.com/open-ag-tech/api-spec/blob/master/versions/light-0.0.1.md#fixture-power)  

### Talking to all fixtures in a zone
```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/fixtures/info
```
Returns an array of [Info](general.md#info-data)  

```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/fixture/[fixtureid]/version  
```
Returns an array of [Version](general.md#version-data)  

```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/fixtures/location
```
Returns an array of [Location](general.md#location-data)  

```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/fixtures/config
```
Returns an array of [Fixture Configuration](https://github.com/open-ag-tech/api-spec/blob/master/versions/light-0.0.1.md#fixture-configuration)  

```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/fixtures/power
```
Returns an array of [Fixture Power](https://github.com/open-ag-tech/api-spec/blob/master/versions/light-0.0.1.md#fixture-power)  

### Fixture Configuration
| Name     | Description                     | Unit  |
| -------- | ------------------------------- | ----- |
| id       | Unique id of the fixture        | uid   |
| channels | array of channel configurations | [Channel Configuration](https://github.com/open-ag-tech/api-spec/blob/master/versions/light-0.0.1.md#channel-configuration) |
### Channel Configuration
| Name      | Description                           | Unit  |
| --------- | ------------------------------------- | ----- |
| id        | Unique id of the channel              | uid   |
| lower     | Lower boundary of the frequency range | nm    |
| upper     | Upper boundary of the frequency range | nm    |
| intensity | Light intensity                       | %     |
### Fixture Power
| Name   | Description                    | Unit          |
| ------ | ------------------------------ | ------------- |
| id     | Unique id of the fixture       | uid           |
| status | The active state of the lights | "on" or "off" |
