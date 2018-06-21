## Example Document Snippets

```yaml
/sensors:
  get:
    description: Returns all sensors from the system that the user has access to
    responses:
      '200':
        description: A list of sensors.
        content:
          application/json:
            schema:
              type: array
              items:
                $ref: '#/components/schemas/Sensor'
/sensors/{sensorId}:
  get:
   summary: Info for a specific sensor
   operationId: showSensorById
   tags:
     - sensors
   parameters:
     - name: sensorId
       in: path
       required: true
       description: The id of the sensor to retrieve
       schema:
         type: string
   responses:
     '200':
       description: Expected response to a valid request
       content:
         application/json:
           schema:
             $ref: "#/components/schemas/Sensors"
     default:
       description: unexpected error
       content:
         application/json:
           schema:
             $ref: "#/components/schemas/Error"  

/sensors/{sensorId}/measurements:
  get:
    description: Returns spectrum measurements from a specific sensor
    parameters:
      - name: format
        in: query
        required: false
        description: PPF or PPFD
        schema:
          type: string
    responses:
      '200':
        description: A list of measurements
        content:
          application/json:
            schema:
              type: array
              items:
                $ref: '#/components/schemas/SpectrumMeasurement'

```

### Example Schema

Sensor

```yaml
type: object
required:
- id
properties:
  name:
    type: string
  info:
    type: string
  version:
    type: string
  location:
    ***TODO: LOCATION FORMAT*** general.md#location-data
  age:
    type: integer
    format: int32
    minimum: 0
```

Measurement

```yaml
type: object
required:
- id
properties:
  id:
    description: Unique id of the device         
    type: string
  timestamp:
    description: UTC timestamp of the measurement
    type: string
  red:
    description: Level of red spectrum light     
    type: string
  blue:
    description: Level of blue spectrum light    
    type: string
  green:
    description: Level of green spectrum light   
    type: string
  uv:
    description: Level of ultraviolet light      
    type: string
  infrared:
    description: Level of infrared light         
    type: string
  par:
    description: Level of absorbable light       
    type: string
  light:
    description: Level of all spectrums of light
    type: string
```

## Example requests

**Retrieving spectrum measurements as PPF**  
```
GET http://[domain:port]/agroapi/[version]/lights/sensors/[sensorid]/ppf  
```
Returns [Light PPF](lights.md#light-ppf)  

**Retrieving spectrum measurements as PPFD**  
```
GET http://[domain:port]/agroapi/[version]/lights/sensors/[sensorid]/ppfd  
```
Returns [Light PPFD](lights.md#light-ppfd)  

### Talking to all sensors
**Retrieving ID information**  
```
GET http://[domain:port]/agroapi/[version]/lights/sensors/info  
```
Returns an array of [Info](general.md#info-data)  

**Sending ID information**  
```
POST http://[domain:port]/agroapi/[version]/lights/sensors/info  
```
Sends an array of [Info](general.md#info-data)  

**Retrieving version information**  
```
GET http://[domain:port]/agroapi/[version]/lights/sensors/version  
```
Returns an array of [Version](general.md#version-data)  

**Retrieving location information**  
```
GET http://[domain:port]/agroapi/[version]/lights/sensors/location  
```
Returns an array of [Location](general.md#location-data)  

**Sending location information**  
```
POST http://[domain:port]/agroapi/[version]/lights/sensors/location  
```
Sends an array of [Location](general.md#location-data)  

**Retrieving spectrum measurements as PPF**  
```
GET http://[domain:port]/agroapi/[version]/lights/sensors/ppf  
```
Returns an array of [Light PPF](lights.md#light-ppf)  

**Retrieving spectrum measurements as PPFD**  
```
GET http://[domain:port]/agroapi/[version]/lights/sensors/ppfd  
```
Returns an array of [Light PPFD](lights.md#light-ppfd)  

### Talking to all sensors in a zone
**Retrieving ID information**  
```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/sensors/info  
```
Returns an array of [Info](general.md#info-data)  

**Sending ID information**  
```
POST http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/sensors/info  
```
Sends an array of [Info](general.md#info-data)  

**Retrieving version information**  
```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/sensors/version  
```
Returns an array of [Version](general.md#version-data)  

**Retrieving location information**  
```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/sensors/location  
```
Returns an array of [Location](general.md#location-data)  

**Sending location information**  
```
POST http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/sensors/location  
```
Sends an array of [Location](general.md#location-data)  

**Retrieving spectrum measurements as PPF**  
```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/sensors/ppf  
```
Returns an array of [Light PPF](lights.md#light-ppf)  

**Retrieving spectrum measurements as PPFD**  
```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/sensors/ppfd  
```
Returns an array of [Light PPFD](lights.md#light-ppfd)  



## Fixtures
### Talking to one fixture
**Retrieving ID information**  
```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/[fixtureid]/info
```
Returns [Info](general.md#info-data)  

**Sending ID information**  
```
POST http://[domain:port]/agroapi/[version]/lights/fixtures/[fixtureid]/info
```
Sends [Info](general.md#info-data)  

**Retrieving version information**  
```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/[fixtureid]/version  
```
Returns [Version](general.md#version-data)  

**Retrieving location information**  
```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/[fixtureid]/location
```
Returns [Location](general.md#location-data)  

**Sending location information**  
```
POST http://[domain:port]/agroapi/[version]/lights/fixtures/[fixtureid]/location
```
Sends [Location](general.md#location-data)  

**Retrieving configuration information**  
```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/[fixtureid]/config
```
Returns [Fixture Configuration](lights.md#fixture-configuration)  

**Sending configuration information**  
```
POST http://[domain:port]/agroapi/[version]/lights/fixtures/[fixtureid]/config
```
Sends [Fixture Configuration](lights.md#fixture-configuration)  

**Retrieving power state information**  
```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/[fixtureid]/power
```
Returns [Fixture Power](lights.md#fixture-power)  

**Sending power state information**  
```
POST http://[domain:port]/agroapi/[version]/lights/fixtures/[fixtureid]/power
```
Sends [Fixture Power](lights.md#fixture-power)  

### Talking to all fixtures
**Retrieving ID information**  
```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/info
```
Returns an array of [Info](general.md#info-data)  

**Sending ID information**  
```
POST http://[domain:port]/agroapi/[version]/lights/fixtures/info
```
Sends an array of [Info](general.md#info-data)  

**Retrieving version information**  
```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/version  
```
Returns an array of [Version](general.md#version-data)  

**Retrieving location information**  
```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/location
```
Returns an array of [Location](general.md#location-data)  

**Sending location information**  
```
POST http://[domain:port]/agroapi/[version]/lights/fixtures/location
```
Sends an array of [Location](general.md#location-data)  

**Retrieving configuration information**  
```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/config
```
Returns an array of [Fixture Configuration](lights.md#fixture-configuration)  

**Sending configuration information**  
```
POST http://[domain:port]/agroapi/[version]/lights/fixtures/config
```
Sends an array of [Fixture Configuration](lights.md#fixture-configuration)  

**Retrieving power state information**  
```
GET http://[domain:port]/agroapi/[version]/lights/fixtures/power
```
Returns an array of [Fixture Power](lights.md#fixture-power)  

**Sending power state information**  
```
POST http://[domain:port]/agroapi/[version]/lights/fixtures/power
```
Sends an array of [Fixture Power](lights.md#fixture-power)  

### Talking to all fixtures in a zone
**Retrieving ID information**  
```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/fixtures/info
```
Returns an array of [Info](general.md#info-data)  

**Sending ID information**  
```
POST http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/fixtures/info
```
Sends an array of [Info](general.md#info-data)  

**Retrieving version information**  
```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/fixture/[fixtureid]/version  
```
Returns an array of [Version](general.md#version-data)  

**Retrieving location information**  
```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/fixtures/location
```
Returns an array of [Location](general.md#location-data)  

**Sending location information**  
```
POST http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/fixtures/location
```
Sends an array of [Location](general.md#location-data)  

**Retrieving configuration information**  
```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/fixtures/config
```
Returns an array of [Fixture Configuration](lights.md#fixture-configuration)  

**Sending configuration information**  
```
POST http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/fixtures/config
```
Sends an array of [Fixture Configuration](lights.md#fixture-configuration)  

**Retrieving power state information**  
```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/fixtures/power
```
Returns an array of [Fixture Power](lghts.md#fixture-power)  

**Sending power state information**  
```
POST http://[domain:port]/agroapi/[version]/zones/[zoneid]/lights/fixtures/power
```
Sends an array of [Fixture Power](lghts.md#fixture-power)  

### Fixture Configuration
| Name     | Description                     | Unit  |
| -------- | ------------------------------- | ----- |
| id       | Unique id of the fixture        | uid   |
| channels | array of channel configurations | [Channel Configuration](lights.md#channel-configuration) |
### Channel Configuration
| Name        | Description                                               | Unit       |
| ----------- | --------------------------------------------------------- | ---------- |
| id          | Unique id of the channel                                  | uid        |
| lo-color    | Lower boundary of the frequency range for a color channel | nm         |
| hi-color    | Upper boundary of the frequency range for a color channel | nm         |
| cct         | Color temperature for a white channel                     | K (Kelvin) |
| intensity   | Light intensity                                           | %          |
### Fixture Power
| Name   | Description                    | Unit          |
| ------ | ------------------------------ | ------------- |
| id     | Unique id of the fixture       | uid           |
| status | The active state of the lights | "on" or "off" |
