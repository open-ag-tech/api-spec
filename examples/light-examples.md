In these examples, we are going to assume that a single greenhouse is being outfitted with a lighting system that uses a wifi-enabled lighting controller (reachable at www.lightcontrol.com).  

The greenhouse is also using a climate control system (reachable at www.climatecontrol.com) that needs to integrate with the lighting system.  

An API token (FA68B23DD511F5A2) has been assigned for integration.  

During planning, the greenhouse has been divided into the following zones...  
* gh1-zone1  
* gh1-zone2  
* gh1-zone3  
* gh1-zone4  
* gh1-zone5  

There are several sensors that have been registered with the lighting control system and are being deployed throughout the zones...  
* LMG-81  
* LMG-82  
* LMG-83  
* LMG-84  
* LMG-85  
* LMG-86  
* LMG-87  
* LMG-88  
* LMG-89  

There are several light fixtures that have been deployed and registered with the lighting control system but they are not yet assigned to zones...  
* FIX-20  
* FIX-21  
* FIX-22  
* FIX-23  
* FIX-24  
* FIX-25  
* FIX-26  
* FIX-27  
* FIX-28  
* FIX-29  
* FIX-30  
* FIX-31  

## Get all fixture IDs and assign them to zones
```
GET www.lightcontrol.com/agroapi/v1/lights/fixtures?token=FA68B23DD511F5A2

//Response
{
  "fixtures": [
    "FIX-20",
    "FIX-21",
    "FIX-22",
    "FIX-23",
    "FIX-24",
    "FIX-25",
    "FIX-26",
    "FIX-27",
    "FIX-28",
    "FIX-29",
    "FIX-30",
    "FIX-31"
    ]
}

POST www.lightcontrol.com/agroapi/v1/lights/zones?token=FA68B23DD511F5A2

// Request
{
  "zones": [{
    "id": "gh1-zone1",
    "fixtures": ["FIX-21","FIX-22"]
    },{
    "id": "gh1-zone2",
    "fixtures": ["FIX-23","FIX-24","FIX-25"]
    },{
    "id": "gh1-zone3",
    "fixtures": ["FIX-26"]
    },{
    "id": "gh1-zone4",
    "fixtures": ["FIX-27","FIX-28"]
    },{
    "id": "gh1-zone5",
    "fixtures": ["FIX-29","FIX-30","FIX-31"]
    }]
}
```

## Light controller pushes measurements for gh1-zone1 to the climate controller  
```
POST www.climatecontrol.com/agroapi/v1/lights/locations/gh1-zone1/measurements?token=FA68B23DD511F5A2
```
**Request**
```json
[{
  "deviceid": "LMG-85",
  "timestamp": "2018-01-25_04-56-05_UTC",
  "red": "1.0",
  "blue": "0.2",
  "green": "0.65",
  "uv": "3",
  "infrared": "0.09",
  "par": "2.16",
  "light": "8.7"
},{
  "deviceid": "LMG-03",
  "timestamp": "2018-01-25_04-56-05_UTC",
  "red": "1.0",
  "blue": "0.2",
  "green": "0.65",
  "uv": "3",
  "infrared": "0.09",
  "par": "5.5",
  "light": "8.7"
}]
```
**Response**  
HTTP status 200  

## Light controller pushes measurements for LMG-85 to the climate controller   
```
POST www.climatecontrol.com/agroapi/v1/lights/devices/LMG-85/measurements?token=FA68B23DD511F5A2
```
**Request**  
```json
{
  "timestamp": "2018-01-25_04-56-05_UTC",
  "red": "1.0",
  "blue": "0.2",
  "green": "0.65",
  "uv": "3",
  "infrared": "0.09",
  "par": "2.16",
  "light": "8.7"
}
```
**Response**  
HTTP status 200  

## Light controller pushes the status for LMG-85 to the climate controller  
```
POST www.climatecontrol.com/agroapi/v1/lights/devices/LMG-85/status?token=FA68B23DD511F5A2
```
**Request**
```json
{
  "timestamp": "2018-01-25_04-56-05_UTC",
  "status": "off"
}
```
**Response**
*HTTP status:* 200

## Climate controller queries measurements for gh1-zone1 from the light controller  
```
GET www.lightcontrol.com/agroapi/v1/lights/locations/gh1-zone1/measurements?token=FA68B23DD511F5A2
```
**Response**  
HTTP status 200  
```json
[{
  "deviceid": "LMG-85",
  "timestamp": "2018-01-25_04-56-05_UTC",
  "red": "1.0",
  "blue": "0.2",
  "green": "0.65",
  "uv": "3",
  "infrared": "0.09",
  "par": "2.16",
  "light": "8.7"
},{
  "deviceid": "LMG-03",
  "timestamp": "2018-01-25_04-56-05_UTC",
  "red": "1.0",
  "blue": "0.2",
  "green": "0.65",
  "uv": "3",
  "infrared": "0.09",
  "par": "5.5",
  "light": "8.7"
}]
```
## Climate controller queries measurements for LMG-85 from the light controller  
```
GET /agroapi/v1/lights/devices/[device_id]/measurements?token=FA68B23DD511F5A2
```
**Response**  
HTTP status 200  
```json
{
  "timestamp": "2018-01-25_04-56-05_UTC",
  "red": "1.0",
  "blue": "0.2",
  "green": "0.65",
  "uv": "3",
  "infrared": "0.09",
  "par": "2.16",
  "light": "8.7"
}
```
## Climate controller queries status for LMG-85 from the light controller  
```
GET /agroapi/v1/lights/devices/LMG-85/status?token=FA68B23DD511F5A2
```
**Response**  
HTTP status 200  
```json
{
  "timestamp": "2018-01-25_04-56-05_UTC",
  "status": "off"
}
```
## Climate controller pushes a common configuration to all fixtures within zone gh1-zone1   
```
POST www.lightcontrol.com/agroapi/v1/lights/locations/gh1-zone1/configuration?token=FA68B23DD511F5A2
```
**Request**  
```json
{
  "channels": [{
    "id": "1",
    "low_nm": "380",
    "high_nm": "450"
  },{
    "id": "2",
    "low_nm": "451",
    "high_nm": "495"
  },{
    "id": "3",
    "low_nm": "496",
    "high_nm": "570"
  },{
    "id": "4",
    "low_nm": "571",
    "high_nm": "590"
  },{
    "id": "5",
    "low_nm": "591",
    "high_nm": "620"
  },{
    "id": "6",
    "low_nm": "621",
    "high_nm": "750"
  }]
}
```
**Response**  
HTTP status 200  

## Climate controller queries the configuration of all fixtures within zone gh1-zone1   
```
GET www.lightcontrol.com/agroapi/v1/lights/locations/gh1-zone1/configuration?token=FA68B23DD511F5A2
```
**Response**  
HTTP status 200  
```json
[{
  "deviceid": "FIX-23",
  "channels": [{
    "id": "1",
    "low_nm": "100",
    "high_nm": "349"
  }]},{
  "deviceid": "FIX-24",
  "channels": [{
    "id": "1",
    "low_nm": "350",
    "high_nm": "750"
  }]},{
  "deviceid": "FIX-25",
  "channels": [{
    "id": "6",
    "low_nm": "751",
    "high_nm": "1000"
  }]
}]
```

