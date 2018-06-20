# API Specification
This specification is intended to define a standardized way of communicating real-time command-and-control data and to allow data collection between control systems and / or peripheral devices.

# Scope

The scope of this document is limited to providing a payload structure and endpoint type definitions to allow basic control and data acquisition. This document does not set out to define an API but rather to specify a uniform way to build one. It does not seek to dictate endpoint names, server architecture, or security protocols.  The addition of product specific features is left to the implementer, but to be in compliance the product must support the basic set of features specified below.

# Definitions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119 of the OpenAPI specification.

# Common Concepts

There are specific concepts that all participants in this open API must support in order to make interaction possible. Each of these concepts should be driven by factory configurations or by on-site configurations made by the customer or a professional integrator.  

Compliance with the Open-Agtech API requires adherence to the OpenAPI Specification (currently [3.0.1](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.1.md)). In addition, there are several principles that account for the needs of our industry.

# URL construction

*Path elements within the URL...*
- The first element of all compliant apis MUST be "agroapi"
- The second element of all compliant apis MUST be the version number
- The third element of all compliant apis MUST be a domain identifier (e.g., "lights", "air", and so on)
- All elements after the third and before the final element are optional and SHOULD describe collections and / or a single member of a collection
- The final element of all compliant apis MUST identify the information or action that is the subject of the call

*Structure of collections...*
- Collection identifiers MUST be plural
- Endpoints SHOULD NOT nest more than 2 collections deep (e.g., collection/{id}/collection/{id})

*Data structures...*
- Individual data points coming from the same device SHOULD be grouped in a structure with other data points that are related to the same topic

# Error Handling

In principle, a successful API call should return an HTTP status code of 200. An unsuccessful API call will return an HTTP status code of 550 and the body should contain an error code that has been properly documented by the owner of the API.  

The interpretation of error codes, including the text describing the error, will be left up to the API user based on their understanding of the error code documentation provided by the API owner.

# Authentication

*TBD* We've agreed on Oauth

# Timestamps

All monitoring data MUST be accompanied by a timestamp in the RFC3339 format.

`YYYY-MM-DDTHH:MM:SS[+8]`

Here is an example of a properly formatted timestamp in UTC:

`2018-01-25T04:56:05Z`

And the same time in the NZST timezone:

`2018-01-25T04:56:05+12:00`

See [http://pretty-rfc.herokuapp.com/RFC3339] for more information.

# Common Structures
Many concepts use the same data structures to report their essential information. Those structures are listed here.  

## Info Data
| Name        | Description                                     | Unit |
| ----------- | ----------------------------------------------- | ---- |
| id          | ID of the entity                                | uid  |
| zone        | ID of the zone containing this entity           | uid  |
| compartment | ID of the compartment that contains this entity | uid  |
| facility    | ID of the facility that contains this entity    | uid  |

## Version Data
| Name    | Description                                | Unit |
| ------- | ------------------------------------------ | ---- |
| id      | unique id of the device                    | uid  |
| make    | Name of the company that makes this device | text |
| model   | Model number of this device                | text |
| version | Version number of this device              | text |

## Location Data
| Name | Description                                             | Unit |
| ---- | ------------------------------------------------------- | ---- |
| id   | Unique id of this entity                                | uid  |
| x    | x coordinate of this entity within its parent container | m    |
| y    | y coordinate of this entity within its parent container | m    |
| z    | z coordinate of this entity within its parent container | m    |

## Dimension Data
| Name   | Description             | Unit |
| ------ | ----------------------- | ---- |
| id     | Unique id of the entity | uid  |
| length | Length of the entity    | m    |
| width  | Width of the entity     | m    |
| height | Height of the entity    | m    |

# Data Types
## Boolean  
Used to express T/F, Y/N, or ON/OFF values   
```json
type: object  
  required:  
    - name  
    - status  
  properties:  
    status:  
    type: bool  
```
## Integer  
Used to express whole 4-byte numbers  
```json
type: object  
  required:  
    - name  
    - value  
  properties:  
    value:  
    type: integer  
```
## Decimal  
Used to express numbers with 8-byte decimal precision  
```json
type: object  
  required:  
    - name  
    - value  
  properties:  
    value:  
      type: number  
      format: double  
```
## String  
Used to send alphanumeric strings  
```json
type: object  
  required:  
    - name  
    - text  
  properties:  
    text:  
      type: string  
```

# Examples

While there are multiple compliant ways to adhere to the API specification, we have compiled examples of API implementations to assist those who may be implementing for the first time.

* [General](general.md) - Examples of common concepts, data structures, timestamp formats, error handling, and so on.
* [Plan](plan.md) - specifies the API for interacting with the basic concepts of a well-planned facility (compartments, zones, crop varieties, and so on)
* [Lights](lights.md) - specifies the API for interacting with lighting systems
* [Air](air.md) - specifies the API for interacting with air control systems (heating, cooling, ventilation, humidity, and so on)
* [Soil](soil.md) - specifies the API for interacting with soil monitoring systems
* [Roots](roots.md) - specifies the API for interacting with root monitoring systems
* [Reservoirs](reservoirs.md) - specifies the API for interacting with reservoir control systems
* [Nutrients](nutrients.md) - specifies the API for monitoring nutrients
