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
