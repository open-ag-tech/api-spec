In these examples, we are going to assume that a single greenhouse is being outfitted with reservoirs and irrigation that connect to a wifi-enabled water control system (reachable at www.watercontrol.com).  

The greenhouse is also using a climate control system (reachable at www.climatecontrol.com) that needs to integrate with the water control system.  

An API token (FA68B23DD511F5A2) has been assigned for integration.  

During planning, the greenhouse has been divided into the following zones...  
* gh1-zone1  
* gh1-zone2  
* gh1-zone3  
* gh1-zone4  
* gh1-zone5  

There are several sensors that have been registered with the air control system and are being deployed throughout the zones...  
* LMG-81  
* LMG-82  
* LMG-83  
* LMG-84  
* LMG-85  
* LMG-86  
* LMG-87  
* LMG-88  
* LMG-89  

There are several controllers that have been deployed and registered with the air control system but they are not yet assigned to zones...  
* TEMP-20  
* TEMP-21  
* TEMP-22  
* TEMP-23  
* TEMP-24  
* TEMP-25  
* TEMP-26  
* TEMP-27  
* TEMP-28  
* TEMP-29  
* TEMP-30  
* TEMP-31  

## Get all fixture IDs and assign them to zones
```
GET www.aircontrol.com/agroapi/v1/air/temperature?token=FA68B23DD511F5A2

//Response
{
  "temperature": [
    "TEMP-20",
    "TEMP-21",
    "TEMP-22",
    "TEMP-23",
    "TEMP-24",
    "TEMP-25",
    "TEMP-26",
    "TEMP-27",
    "TEMP-28",
    "TEMP-29",
    "TEMP-30",
    "TEMP-31"
    ]
}

POST www.aircontrol.com/agroapi/v1/air/zones?token=FA68B23DD511F5A2

// Request
{
  "zones": [{
    "id": "gh1-zone1",
    "fixtures": ["TEMP-21","TEMP-22"]
    },{
    "id": "gh1-zone2",
    "fixtures": ["TEMP-23","TEMP-24","TEMP-25"]
    },{
    "id": "gh1-zone3",
    "fixtures": ["TEMP-26"]
    },{
    "id": "gh1-zone4",
    "fixtures": ["TEMP-27","TEMP-28"]
    },{
    "id": "gh1-zone5",
    "fixtures": ["TEMP-29","TEMP-30","TEMP-31"]
    }]
}
```

### Sensor Collection
#### Push APIs - Real-time Measurements
##### All Device Data
**URL**
```
POST /agroapi/v1/reservoir/locations/[location_id]/measurements?token=[api_token]
```
**Request Payload**
```json
[{
  "deviceid": "LMG-85",
  "timestamp": "2018-01-25_04-56-05_UTC",
  "water": "72.5"
  "temp": "23.45",
  "turbidity": "0.3",
  "oxygen": "20567",
  "ec": "1200",
  "ph": "7.3"
},{
  "deviceid": "LMG-03",
  "timestamp": "2018-01-25_04-56-05_UTC",
  "water": "72.5"
  "temp": "23.45",
  "turbidity": "0.3",
  "oxygen": "20567",
  "ec": "1200",
  "ph": "7.3"
}]
```
**Response Payload**
```json
200:
{
}
400:
{
  "error": "<code>"
}
```

##### Single Device Data
**URL**
```
POST /agroapi/v1/reservoir/locations/[location_id]/devices/[device_id]/measurements?token=[api_token]
```
**Request Payload**
```json
{
  "timestamp": "2018-01-25_04-56-05_UTC",
  "water": "72.5"
  "temp": "23.45",
  "turbidity": "0.3",
  "oxygen": "20567",
  "ec": "1200",
  "ph": "7.3"
}
```
**Response Payload**
```json
200:
{
}
400:
{
  "error":"<code>"
}
```
##### Single Device Status
**URL**
```
POST /agroapi/v1/reservoir/locations/[location_id]/devices/[device_id]/status?token=[api_token]
```
**Request Payload**
```json
{
  "timestamp": "2018-01-25_04-56-05_UTC",
  "off": "false"
}
```
**Response Payload**
```json
200:
{
}
400:
{
  "error":"<code>"
}
```
#### Pull APIs - Real-time Measurements
##### All Device Data
**URL**
```
GET /agroapi/v1/reservoir/locations/[location_id]/measurements?token=[api_token]
```
**Request Payload**
```json
{}
```
**Response Payload**
```json
200:
[{
  "deviceid": "LMG-85",
  "timestamp": "2018-01-25_04-56-05_UTC",
  "water": "72.5"
  "temp": "23.45",
  "turbidity": "0.3",
  "oxygen": "20567",
  "ec": "1200",
  "ph": "7.3"
},{
  "deviceid": "LMG-03",
  "timestamp": "2018-01-25_04-56-05_UTC",
  "water": "72.5"
  "temp": "23.45",
  "turbidity": "0.3",
  "oxygen": "20567",
  "ec": "1200",
  "ph": "7.3"
}]
400:
{
  "error":"<code>"
}
```
##### Single Device Data
**URL**
```
GET /agroapi/v1/reservoir/locations/[location_id]/devices/[device_id]/measurements?token=[api_token]
```
**Request Payload**
```json
{}
```
**Response Payload**
```json
200:
{
  "timestamp": "2018-01-25_04-56-05_UTC",
  "water": "72.5"
  "temp": "23.45",
  "turbidity": "0.3",
  "oxygen": "20567",
  "ec": "1200",
  "ph": "7.3"
}
400:
{
  "error":"<code>"
}
```
##### Single Device Status
**URL**
```
GET /agroapi/v1/reservoir/locations/[location_id]/devices/[device_id]/status?token=[api_token]
```
**Request Payload**
```json
{}
```
**Response Payload**
```json
200:
{
  "timestamp": "2018-01-25_04-56-05_UTC",
  "off": "false"
}
400:
{
  "error":"<code>"
}
```