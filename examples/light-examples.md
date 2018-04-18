In these examples, we are going to assume the following...  

* There are several pre-defined zones in the greenhouse...  
** gh1-zone1  
** gh1-zone2  
** gh1-zone3  
* There are several sensors deployed in zone 1...  
** LMG-85  
** LMG-86  
** LMG-87  
* There are several light fixtures deployed in zone 1...  
** FIX-23  
** FIX-24  
** FIX-25  
* The other 2 zones the same number of sensors and fixtures as zone 1  
* An API token has been assigned for authentication...  
** FA68B23DD511F5A2  
* The light controller is reachable at www.lightcontrol.com
* The climate controller is reachable at www.climatecontrol.com  

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

