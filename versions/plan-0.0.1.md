# Purpose

This specification is intended to define a standardized way of communicating with facility planning systems for planning the layout of a facility and the deployment of monitoring and control systems.

# Scope

The scope of this document is limited to providing a payload structure and endpoint type definitions to allow basic control and data acquisition. The addition of product specific features is left to the implementer, but to be in compliance the product must support the basic set of features specified below.

# Definitions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

# Endpoints
The relationship between the common concepts (facilities, compartments, zones, etc) is maintained as part of a Plan that can be interrogated. The following URLs MUST be supported by any service that wishes to interact with a Plan.

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
Returns an array of [Info](https://github.com/open-ag-tech/api-spec/blob/master/versions/0.0.1.md#info)  

```
GET http://[domain:port]/agroapi/[version]/plan/compartments/location  
```
Returns an array of [Location](https://github.com/open-ag-tech/api-spec/blob/master/versions/0.0.1.md#location)  
```
GET http://[domain:port]/agroapi/[version]/plan/compartments/dimensions  
```
Returns an array of [Dimensions](https://github.com/open-ag-tech/api-spec/blob/master/versions/0.0.1.md#dimensions)  


### Single compartment
```
GET http://[domain:port]/agroapi/[version]/plan/compartments/[compartmentid]/info  
```
Returns [Info](https://github.com/open-ag-tech/api-spec/blob/master/versions/0.0.1.md#info)  

```
GET http://[domain:port]/agroapi/[version]/plan/compartments/[compartmentid]/location  
```
Returns [Location](https://github.com/open-ag-tech/api-spec/blob/master/versions/0.0.1.md#location)  

```
GET http://[domain:port]/agroapi/[version]/plan/compartments/[compartmentid]/dimensions  
```
Returns [Dimensions](https://github.com/open-ag-tech/api-spec/blob/master/versions/0.0.1.md#dimensions)  

```
GET http://[domain:port]/agroapi/[version]/plan/compartment/[compartmentid]/zones  
```
Returns an array of [Info](https://github.com/open-ag-tech/api-spec/blob/master/versions/0.0.1.md#info)  

## Zones
### All zones
```
GET http://[domain:port]/agroapi/[version]/plan/zones/info  
```
Returns an array of [Info](https://github.com/open-ag-tech/api-spec/blob/master/versions/0.0.1.md#info)  

```
GET http://[domain:port]/agroapi/[version]/plan/zones/location  
```
Returns an array of [Location](https://github.com/open-ag-tech/api-spec/blob/master/versions/0.0.1.md#location)  

```
GET http://[domain:port]/agroapi/[version]/plan/zones/dimensions  
```
Returns an array of [Dimensions](https://github.com/open-ag-tech/api-spec/blob/master/versions/0.0.1.md#dimensions)  

### Single zone
```
GET http://[domain:port]/agroapi/[version]/plan/zones/[zoneid]/info  
```
Returns [Info](https://github.com/open-ag-tech/api-spec/blob/master/versions/0.0.1.md#info)  

```
GET http://[domain:port]/agroapi/[version]/plan/zones/[zoneid]/location  
```
Returns [Location](https://github.com/open-ag-tech/api-spec/blob/master/versions/0.0.1.md#location)  

```
GET http://[domain:port]/agroapi/[version]/plan/zones/[zoneid]/dimensions  
```
Returns [Dimensions](https://github.com/open-ag-tech/api-spec/blob/master/versions/0.0.1.md#dimensions)  

```
GET http://[domain:port]/agroapi/[version]/plan/zones/[zoneid]/zones  
```
Returns an array of Zone IDs  

```
GET http://[domain:port]/agroapi/[version]/plan/zones/[zoneid]/crops  
```
Returns an array of Crop Variety IDs  
