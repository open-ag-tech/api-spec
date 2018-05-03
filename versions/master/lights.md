# Examples: Lights

# Endpoints
## Sensors
### Talking to one sensor
```
GET http://[domain:port]/agroapi/[version]/lights/sensors/[sensorid]/info  
```
Returns [Info](README.md#info-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/sensors/[sensorid]/version  
```
Returns [Version](README.md#version-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/sensors/[sensorid]/location  
```
Returns [Location](README.md#location-data)  

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
Returns an array of [Info](README.md#info-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/sensors/version  
```
Returns an array of [Version](README.md#version-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/sensors/location  
```
Returns an array of [Location](README.md#location-data)  

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
Returns an array of [Info](README.md#info-data)  

```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/sensors/version  
```
Returns an array of [Version](README.md#version-data)  

```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/sensors/location  
```
Returns an array of [Location](README.md#location-data)  

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
Returns [Info](README.md#info-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/[fixtureid]/version  
```
Returns [Version](README.md#version-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/[fixtureid]/location
```
Returns [Location](README.md#location-data)  

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
Returns an array of [Info](README.md#info-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/version  
```
Returns an array of [Version](README.md#version-data)  

```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/location
```
Returns an array of [Location](README.md#location-data)  

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
Returns an array of [Info](README.md#info-data)  

```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/fixture/[fixtureid]/version  
```
Returns an array of [Version](README.md#version-data)  

```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/fixtures/location
```
Returns an array of [Location](README.md#location-data)  

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
