## Example Document Snippets

```yaml
/light_sensors:
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
/light_sensors/{sensorId}:
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
             type: array
             items:
               $ref: "#/components/schemas/Sensors"
     default:
       description: unexpected error
       content:
         application/json:
           schema:
             $ref: "#/components/schemas/Error"  

/light_sensors/{sensorId}/measurements:
  get:
    description: Returns spectrum measurements from a specific sensor
    parameters:
      - name: type
        in: query
        required: false
        description: ppf or ppfd, defaults to ppfd
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

/zone/{zoneId}/sensors:
  get:
    description: Returns all sensors from a zone
    responses:
      '200':
        description: A list of sensors.
        content:
          application/json:
            schema:
              type: array
              items:
                $ref: '#/components/schemas/Sensor'

light_sensors:
  get:
    description: Returns all sensors from a zone
    responses:
      '200':
        description: A list of sensors.
        content:
          application/json:
            schema:
              type: array
              items:
                $ref: '#/components/schemas/Sensor'

light_fixtures:
  get:
    description: Returns all fixtures that a user has access to
    responses:
      '200':
        description: A list of fixtures.
        content:
          application/json:
            schema:
              type: array
              items:
                $ref: '#/components/schemas/Fixture'

/light_fixtures/{fixtureId}:
  get:
    summary: Info for a specific fixture
    operationId: showFixtureById
    tags:
      - fixtures
    parameters:
      - name: fixtureId
        in: path
        required: true
        description: The id of the fixture to retrieve
        schema:
          type: string
    responses:
      '200':
        description: Expected response to a valid request
        content:
          application/json:
            schema:
              type: array
              items:
                $ref: "#/components/schemas/Fixture"


/light_fixtures/{fixtureId}/light_channels:
  get:
    description: Returns all channels from a fixture
    responses:
      '200':
        description: A list of channels.
        content:
          application/json:
            schema:
              type: array
              items:
                $ref: '#/components/schemas/Channel'
```

## Example Schema

### Sensor

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
  info:
    ***TODO: INFO FORMAT*** general.md#info-data
  age:
    type: integer
    format: int32
    minimum: 0
```

### Measurement

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

### Fixture

```yaml
type: object
required:
- id
- status
properties:
  id:
    description: Unique id of the fixture
    type: string
  name:
    type: string
  status:
    description: The active state of the light ('on' or 'off')
    type: string
```

```yaml
type: object
required:
- id
properties:
  name:
    type: string
  status:
    description: The active state of the light ('on' or 'off')
    type: string
```

### Channel

```yaml
type: object
required:
- id
properties:
  id:
    description: Unique id of the channel
  lo-color:
    description: Lower boundary of the frequency range for a color channel
    format: ***TODO FORMAT nm***
  hi-color:
    description: Upper boundary of the frequency range for a color channel
    format: ***TODO FORMAT nm***
  cct:
    description: Color temperature for a white channel
    format: ***TODO FORMAT K (Kelvin)***
  intensity:
    description: Light intensity
    format: ***TODO FORMAT %***
```


## Example requests

### Sensors

**Retrieving sensor information**
```
GET http://[domain:port]/agroapi/[version]/light_sensors/[sensorid]
```

**Updating sensor information**
```
PUT http://[domain:port]/agroapi/[version]/light_sensors/[sensorid]
```

**Retrieving spectrum measurements as PPF**
```
GET http://[domain:port]/agroapi/[version]/light_sensors/[sensorid]/measurements?type=ppf
```

**Retrieving spectrum measurements as PPFD**
```
GET http://[domain:port]/agroapi/[version]/light_sensors/[sensorid]/measurements?type=ppf
```

**Retrieving information for all sensors**
```
GET http://[domain:port]/agroapi/[version]/light_sensors
```

**Retrieving information for all sensors in a zone**
```
GET http://[domain:port]/agroapi/[version]/zones/[zoneid]/light_sensors
```


### Fixtures

**Retrieving information for all fixtures**
```
GET http://[domain:port]/agroapi/[version]/light_fixtures
```

**Retrieving information for a fixture**
```
GET http://[domain:port]/agroapi/[version]/light_fixtures/[fixtureid]
```

**Updating information for a fixture**
```
PUT http://[domain:port]/agroapi/[version]/light_fixtures/[fixtureid]
```


### Channels

**Retrieving channel configurations for a fixture**
```
GET http://[domain:port]/agroapi/[version]/light_fixtures/[fixture_id]/light_channels
```

**Updating channel configuration**
```
PUT http://[domain:port]/agroapi/[version]/light_channels/[channel_id]
```
