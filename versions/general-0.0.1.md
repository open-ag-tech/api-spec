# Purpose

This specification is intended to define a standardized way of communicating real-time command-and-control data and to allow data collection between control systems and / or peripheral devices.

# Scope

The scope of this document is limited to providing a payload structure and endpoint type definitions to allow basic control and data acquisition. This document does not set out to define an API but rather to specify a uniform way to build one. It does not seek to dictate endpoint names, server architecture, or security protocols.  The addition of product specific features is left to the implementer, but to be in compliance the product must support the basic set of features specified below.

# Definitions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

# Common Concepts

There are specific concepts that all participants in this open API must support in order to make interaction possible. Each of these concepts should be driven by factory configurations or by on-site configurations made by the customer or a professional integrator.  
The diagram below captures their essential relationships.  

![Common Concepts](https://docs.google.com/drawings/d/e/2PACX-1vRptSa5X7K6yzOqA95Jpncwwl8rUZgxOo6l13m_VcnCyd5dHmlLZvUyrED-HX2b5Q9YNHiBltB6cY5t/pub?w=982&h=1042)

## Company

A company refers to a single entity that owns and operates one or more facilities. Each company makes its own purchasing and planning decisions and has only one set of executives.

## System

Every company has one or more systems that are helping to control all activity related to agriculture (e.g., Argus, Lumigrow, Priva, and so on). In order to help identify compatibility levels, each system should be able to report its make and model number as well as a version number related to its embedded software. Each system can own one or more systems and / or devices and must be able to accept calls on behalf of its devices. For example, a large climate control system might own a network of light and air sensors while also controlling lighting, ventilation and irrigation systems. Systems can manage devices across zones and crops.

## Crop Variety

A crop refers to one or more types of plants that are being grown in the same environment - i.e., if a single greenhouse is inter-planting strawberries and mint, this would be considered a single crop for the purposes of management and prediction. Crop variety IDs do not need to be standardized, so long as they are consistent within a single company.  

## Facility

A facility is a single physical site that contains one or more compartments - e.g., a greenhouse. A company can own many facilities and each facility will have one or more Head Growers to oversee its operations.

## Compartment

A compartment is a physically isolated space within a facility for the purpose of establishing a unique macro climate. Each compartment is dedicated to one or more crop varieties. Every compartment has a length, width and height. By default, every compartment contains a single zone that is the length, width, and height of the compartment.

## Zone

A zone identifies an area within a compartment dedicated to maintaining a micro-climate. For example, a compartment would maintain uniform levels of humidity and air temperature, whereas a zone might alter the light levels or nutrient mix in the irrigation to create unique micro-climates.  

Every zone contains zero or more zones and / or devices. Every device that is deployed should be assigned to the correct zone. Zones are a natural way of grouping devices for control purposes, so that a configuration can be pushed to a zone and affect all relevant devices within the zone at the same time.  

All zones must be able to identify the crop variety they are overseeing. All data produced from a zone must include a crop variety ID for easy identification.  

Each zone must be able to identify its size (in width and height) as well as its relative location within the compartment, since all sensors and controllers within that zone will report their location relative to the zone, not the compartment.  

Zones can be combined into deep hierarchies. For example, a compartment can have multiple rows of plants that are 1 foot off the floor (e.g., lettuce), with an additional layer of plants 4 feet off the floor (e.g., strawberries). The grower would want to create unique zones for the lettuce vs. the strawberries, reflecting their unique feeds for irrigation and supplemental lighting. However, the grower would also want to maintain a general climate zone for the overall compartment for the purposes of controlling heating and ventilation. This means that the compartment would have a global zone containing two sub-zones.  

## Location

Every device and zone should know its position relative to its container (devices are contained by zones, zones are contained by compartments). Locations are described using x, y, and z co-ordinates (or length, width, and height).  

## Device

A device refers to any physical mechanism that can either monitor or control the growing environment (lights, pumps, heaters, humidifiers, etc).  

Every device must be related to a zone and a location within that zone. It should be able to report these relationships along with its own unique ID.  

## Sensor

A sensor refers to any device that is gathering data about the growing environment (light, air, water, nutrients, and so on).  

## Controller

A controller refers to any device that can affect the growing environment (light fixtures, nutrient dosers, heaters, humidifiers, and so on).  

# Endpoint Structure

The detailed endpoint structure is outside the scope of this document because it needs to make sense for the overall architecture of the implementation. However, there are a few standards that need to be considered when it comes to endpoint design.  

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

**Example**

GET https://www.googleapis.com/books/v1/volumes/zyTCAlFPjgYC?key=yourAPIKey

# Error Handling

In principle, a successful API call should return an HTTP status code of 200. An unsuccessful API call will return an HTTP status code of 550 and the body should contain an error code that has been properly documented by the owner of the API.  

The interpretation of error codes, including the text describing the error, will be left up to the API user based on their understanding of the error code documentation provided by the API owner.

# Validation Handshake

*TBD*

Although a data consumer / receiver will have its own limits when it comes to value ranges and so on, there is a perceived need for the consumer / receiver to know what value ranges the data producer / sender might provide. This gives the consumer / receiver a secondary validation check to ensure that the data makes sense.

# Timestamps

All monitoring data MUST be accompanied by a timestamp that includes year, month, day, hour, minute, second, and time zone. The format MUST be as follows…

```[year]-[month]-[day]_[hour]-[min]-[sec]_[timezone]```

Here is an example of a properly formatted timestamp…

```2018-01-25_04-56-05_UTC```

# Common Structures
Many concepts use the same data structures to report their essential information. Those structures are listed here.  

## Info
| Name        | Description                                     | Unit |
| ----------- | ----------------------------------------------- | ---- |
| id          | ID of the entity                                | uid  |
| zone        | ID of the zone containing this entity           | uid  |
| compartment | ID of the compartment that contains this entity | uid  |
| facility    | ID of the facility that contains this entity    | uid  |

## Version
| Name    | Description                                | Unit |
| ------- | ------------------------------------------ | ---- |
| id      | unique id of the device                    | uid  |
| make    | Name of the company that makes this device | text |
| model   | Model number of this device                | text |
| version | Version number of this device              | text |

## Location
| Name | Description                                             | Unit |
| ---- | ------------------------------------------------------- | ---- |
| id   | Unique id of this entity                                | uid  |
| x    | x coordinate of this entity within its parent container | m    |
| y    | y coordinate of this entity within its parent container | m    |
| z    | z coordinate of this entity within its parent container | m    |

## Dimensions
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

# Primitive Endpoints
The following endpoints provide examples of payloads that would be exchanged for any endpoints that are trying to work with simple primitive values (e.g., a single number, boolean flag, or piece of text).

Request and response bodies are presented below in JSON as well as YAML (which is compatible with OpenAPI 3.0).
NOTE: proper RESTful URLs should contain the identification of the entities being queries or acted upon (names or IDs) in the URL itself. Therefore, those identifications do not show up in the payloads.

## Integer
**Operation:** GET  
Fetches an integer entry. This will fail if the integer entry does not yet exist.  
**Request Body**  
None  
**Response Body**  
YAML  
```
responses:
  '200':
    description: successful operation
    content:
      application/json:
        schema:
          type: object
          required:
          - value
          properties:
            value:
              type: integer    
            links:
              type: array
              items:
                type: string
  '400':
    description: Failure
    content:
      application/json:
        schema:
          type: object
          required:
            - error
          properties:
            error:
              type: integer
          links:
            type: array
            items:
              type: string
```
JSON  
```json
200:
{
  "value": "<integer>",
  "links": [{"<string>"},{"..."}]
}
400:
{
  "error": "<code>",
  "links": [{"<string>"},{"..."}]
}
```

**Operation:** POST  
Updates an existing integer entry. This will fail if the integer entry does not yet exist.  
**Request Body**  
YAML  
```
required: true
  content:
    application/json:
      schema:
        type: object
        required:
          - value
        properties:
          value:
            type: integer
```
JSON  
```json
{
  "value": "<integer>"
}
```
**Response Body**  
YAML  
```
responses:
  '200':
    description: Success
    content:
      application/json:
        schema:
          type: object
            links:
              type: array
              items:
                type: string
  '400':
    description: Failure
    content:
      application/json:
        schema:
          type: object
          required:
            - error
          properties:
            error:
              type: integer
          links:
            type: array
            items:
              type: string
```
JSON  
```json
200:
{
  "links": [{"<string>"},{"..."}]
}
400:
{
  "error": "<code>",
  "links": [{"<string>"},{"..."}]
}
```
**Operation:** PUT  
Creates a new integer entry. This will fail if the integer entry already exists.  
**Request Body**  
YAML  
```
required: true
  content:
    application/json:
      schema:
        type: object
        required:
          - value
        properties:
          value:
            type: integer
```
JSON  
```json
{
  "value": "<integer>"
}
```
**Response Body**  
YAML  
```
responses:
  '200':
    description: Success
    content:
      application/json:
        schema:
          type: object        
          properties:
            links:
              type: array
                items:
                  type: string
  '400':
    description: Failure
    content:
      application/json:
        schema:
          type: object
          required:
            - error
          properties:
            error:
              type: integer
          links:
            type: array
            items:
              type: string
```
JSON  
```json
200:
{
  "links": [{"<string>"},{"..."}]
}
400:
{
  "error": "<code>",
  "links": [{"<string>"},{"..."}]
}
```
**Operation:** DELETE  
Deletes an existing integer entry. This will fail if the integer entry does not already exist.  
**Request Body**  
None  
**Response Body**  
YAML  
```
responses:
  '200':
    description: Success
    content:
      application/json:
        schema:
          type: object        
          properties:
            links:
              type: array
                items:
                  type: string
  '400':
    description: Failure
    content:
      application/json:
        schema:
          type: object
          required:
            - error
          properties:
            error:
              type: integer
          links:
            type: array
            items:
              type: string
```
JSON  
```json
200:
{
  "links": [{"<string>"},{"..."}]
}
400:
{
  "error": "<code>",
  "links": [{"<string>"},{"..."}]
}
```
## Decimal  
**Operation:** GET  
Fetches a decimal entry. This will fail if the decimal entry does not yet exist.  
**Request Body**  
None  
**Response Body**  
YAML  
```
responses:
  '200':
    description: successful operation
    content:
      application/json:
        schema:
          type: object
          required:
          - value
          properties:
            value:
              type: double    
            links:
              type: array
              items:
                type: string
  '400':
    description: Failure
    content:
      application/json:
        schema:
          type: object
          required:
            - error
          properties:
            error:
              type: integer
          links:
            type: array
            items:
              type: string
```
JSON  
```json
200:
{
  "value": "<double>",
  "links": [{"<string>"},{"..."}]
}
400:
{
  "error": "<code>",
  "links": [{"<string>"},{"..."}]
}
```
**Operation:** POST  
Updates an existing decimal entry. This will fail if the decimal entry does not yet exist.  
**Request Body**  
YAML  
```
required: true
  content:
    application/json:
      schema:
        type: object
        required:
          - value
        properties:
          value:
            type: double
```
JSON  
```json
{
  "value": "<double>"
}
```
**Response Body**  
YAML  
```
responses:
  '200':
    description: Success
    content:
      application/json:
        schema:
          type: object
            links:
              type: array
              items:
                type: string
  '400':
    description: Failure
    content:
      application/json:
        schema:
          type: object
          required:
            - error
          properties:
            error:
              type: integer
          links:
            type: array
            items:
              type: string
```
JSON
```json
200:
{
  "links": [{"<string>"},{"..."}]
}
400:
{
  "error": "<code>",
  "links": [{"<string>"},{"..."}]
}
```
**Operation:** PUT  
Creates a new decimal entry. This will fail if the decimal entry already exists.  
**Request Body**  
YAML  
```
required: true
  content:
    application/json:
      schema:
        type: object
        required:
          - value
        properties:
          value:
            type: double
```
JSON  
```json
{
  "value": "<double>"
}
```
**Response Body**  
YAML  
```
responses:
  '200':
    description: Success
    content:
      application/json:
        schema:
          type: object        
          properties:
            links:
              type: array
                items:
                  type: string
  '400':
    description: Failure
    content:
      application/json:
        schema:
          type: object
          required:
            - error
          properties:
            error:
              type: integer
          links:
            type: array
            items:
              type: string
```
JSON
```json
200:
{
  "links": [{"<string>"},{"..."}]
}
400:
{
  "error": "<code>",
  "links": [{"<string>"},{"..."}]
}
```
**Operation:** DELETE  
Deletes an existing decimal entry. This will fail if the decimal entry does not already exist.  
**Request Body**  
None  
**Response Body**  
YAML  
```
responses:
  '200':
    description: Success
    content:
      application/json:
        schema:
          type: object        
          properties:
            links:
              type: array
                items:
                  type: string
  '400':
    description: Failure
    content:
      application/json:
        schema:
          type: object
          required:
            - error
          properties:
            error:
              type: integer
          links:
            type: array
            items:
              type: string
```
JSON  
```json
200:
{
  "links": [{"<string>"},{"..."}]
}
400:
{
  "error": "<code>",
  "links": [{"<string>"},{"..."}]
}
```
## String  
**Operation:** GET  
Fetches a string entry. This will fail if the string entry does not yet exist  
**Request Body**  
None  
**Response Body**  
YAML  
```
responses:
  '200':
    description: successful operation
    content:
      application/json:
        schema:
          type: object
          required:
          - value
          properties:
            value:
              type: string    
            links:
              type: array
              items:
                type: string
  '400':
    description: Failure
    content:
      application/json:
        schema:
          type: object
          required:
            - error
          properties:
            error:
              type: integer
          links:
            type: array
            items:
              type: string
```
JSON  
```json
200:
{
  "value": "<string>",
  "links": [{"<string>"},{"..."}]
}
400:
{
  "error": "<code>",
  "links": [{"<string>"},{"..."}]
}
```

**Operation:** POST  
Updates an existing string entry. This will fail if the string entry does not yet exist.  
**Request Body**  
YAML  
```
required: true
  content:
    application/json:
      schema:
        type: object
        required:
          - value
        properties:
          value:
            type: string
```
JSON  
```json
{
  "value": "<string>"
}
```
**Response Body**  
YAML  
```
responses:
  '200':
    description: Success
    content:
      application/json:
        schema:
          type: object
            links:
              type: array
              items:
                type: string
  '400':
    description: Failure
    content:
      application/json:
        schema:
          type: object
          required:
            - error
          properties:
            error:
              type: integer
          links:
            type: array
            items:
              type: string
```
JSON  
```json
200:
{
  "links": [{"<string>"},{"..."}]
}
400:
{
  "error": "<code>",
  "links": [{"<string>"},{"..."}]
}
```
**Operation:** PUT  
Creates a new string entry. This will fail if the string entry already exists.  
**Request Body**  
YAML  
```
required: true
  content:
    application/json:
      schema:
        type: object
        required:
          - value
        properties:
          value:
            type: string
```
JSON  
```json
{
  "value": "<string>"
}
```
**Response Body**  
YAML  
```
responses:
  '200':
    description: Success
    content:
      application/json:
        schema:
          type: object        
          properties:
            links:
              type: array
                items:
                  type: string
  '400':
    description: Failure
    content:
      application/json:
        schema:
          type: object
          required:
            - error
          properties:
            error:
              type: integer
          links:
            type: array
            items:
              type: string
```
JSON  
```json
200:
{
  "links": [{"<string>"},{"..."}]
}
400:
{
  "error": "<code>",
  "links": [{"<string>"},{"..."}]
}
```
**Operation:** DELETE  
Deletes an existing string entry. This will fail if the string entry does not already exist.  
**Request Body**  
None  
**Response Body**  
YAML  
```
responses:
  '200':
    description: Success
    content:
      application/json:
        schema:
          type: object        
          properties:
            links:
              type: array
                items:
                  type: string
  '400':
    description: Failure
    content:
      application/json:
        schema:
          type: object
          required:
            - error
          properties:
            error:
              type: integer
          links:
            type: array
            items:
              type: string
```
JSON
```json
200:
{
  "links": [{"<string>"},{"..."}]
}
400:
{
  "error": "<code>",
  "links": [{"<string>"},{"..."}]
}
```
