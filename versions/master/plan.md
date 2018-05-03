# Examples: Plan

# Endpoints
The relationship between the common concepts (facilities, compartments, zones, etc) is maintained as part of a Plan that can be interrogated.

## Facilities
### All facilities
```
GET http://[domain:port]/agroapi/[version]/plan/facilities  
```
Returns an array of Facility IDs  

### Single facility
```
GET http://[domain:port]/agroapi/[version]/plan/facilities/[facilityid]/compartments  
```
Returns an array of Compartment IDs  

```
GET http://[domain:port]/agroapi/[version]/plan/facilities/[facilityid]/zones  
```
Returns an array of Zone IDs  

## Compartments
### All compartments
```
GET http://[domain:port]/agroapi/[version]/plan/compartments  
```
Returns an array of Compartment IDs  

```
GET http://[domain:port]/agroapi/[version]/plan/compartments/info  
```
Returns an array of [Info](https://github.com/open-ag-tech/api-spec/blob/master/versions/general-0.0.1.md#info-data)  

```
GET http://[domain:port]/agroapi/[version]/plan/compartments/location  
```
Returns an array of [Location](https://github.com/open-ag-tech/api-spec/blob/master/versions/general-0.0.1.md#location-data)  
```
GET http://[domain:port]/agroapi/[version]/plan/compartments/dimensions  
```
Returns an array of [Dimensions](https://github.com/open-ag-tech/api-spec/blob/master/versions/general-0.0.1.md#dimension-data)  


### Single compartment
```
GET http://[domain:port]/agroapi/[version]/plan/compartments/[compartmentid]/info  
```
Returns [Info](https://github.com/open-ag-tech/api-spec/blob/master/versions/general-0.0.1.md#info-data)  

```
GET http://[domain:port]/agroapi/[version]/plan/compartments/[compartmentid]/location  
```
Returns [Location](https://github.com/open-ag-tech/api-spec/blob/master/versions/general-0.0.1.md#location-data)  

```
GET http://[domain:port]/agroapi/[version]/plan/compartments/[compartmentid]/dimensions  
```
Returns [Dimensions](https://github.com/open-ag-tech/api-spec/blob/master/versions/general-0.0.1.md#dimension-data)  

```
GET http://[domain:port]/agroapi/[version]/plan/compartment/[compartmentid]/zones  
```
Returns an array of [Info](https://github.com/open-ag-tech/api-spec/blob/master/versions/general-0.0.1.md#info-data)  

## Zones
### All zones
```
GET http://[domain:port]/agroapi/[version]/plan/zones/info  
```
Returns an array of [Info](https://github.com/open-ag-tech/api-spec/blob/master/versions/general-0.0.1.md#info-data)  

```
GET http://[domain:port]/agroapi/[version]/plan/zones/location  
```
Returns an array of [Location](https://github.com/open-ag-tech/api-spec/blob/master/versions/general-0.0.1.md#location-data)  

```
GET http://[domain:port]/agroapi/[version]/plan/zones/dimensions  
```
Returns an array of [Dimensions](https://github.com/open-ag-tech/api-spec/blob/master/versions/general-0.0.1.md#dimension-data)  

### Single zone
```
GET http://[domain:port]/agroapi/[version]/plan/zones/[zoneid]/info  
```
Returns [Info](https://github.com/open-ag-tech/api-spec/blob/master/versions/general-0.0.1.md#info-data)  

```
GET http://[domain:port]/agroapi/[version]/plan/zones/[zoneid]/location  
```
Returns [Location](https://github.com/open-ag-tech/api-spec/blob/master/versions/general-0.0.1.md#location-data)  

```
GET http://[domain:port]/agroapi/[version]/plan/zones/[zoneid]/dimensions  
```
Returns [Dimensions](https://github.com/open-ag-tech/api-spec/blob/master/versions/general-0.0.1.md#dimension-data)  

```
GET http://[domain:port]/agroapi/[version]/plan/zones/[zoneid]/zones  
```
Returns an array of Zone IDs  

```
GET http://[domain:port]/agroapi/[version]/plan/zones/[zoneid]/crops  
```
Returns an array of Crop Variety IDs  
