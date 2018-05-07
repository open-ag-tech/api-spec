# Examples: General

The diagram below captures a common structure of a company with several facilities. This document gives examples on a way in which the API could be implemented within that system.

![Common Structure](https://docs.google.com/drawings/d/e/2PACX-1vRptSa5X7K6yzOqA95Jpncwwl8rUZgxOo6l13m_VcnCyd5dHmlLZvUyrED-HX2b5Q9YNHiBltB6cY5t/pub?w=982&h=1042)

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

In this example, zones identify the crop variety they are overseeing, and include a crop variety ID for easy identification.  

Each zone identifies its size (in width and height) as well as its relative location within the compartment, since all sensors and controllers within that zone will report their location relative to the zone, not the compartment.  

Zones can be combined into deep hierarchies. For example, a compartment can have multiple rows of plants that are 1 foot off the floor (e.g., lettuce), with an additional layer of plants 4 feet off the floor (e.g., strawberries). The grower would want to create unique zones for the lettuce vs. the strawberries, reflecting their unique feeds for irrigation and supplemental lighting. However, the grower would also want to maintain a general climate zone for the overall compartment for the purposes of controlling heating and ventilation. This means that the compartment would have a global zone containing two sub-zones.  

## Location

Every device and zone should know its position relative to its container (devices are contained by zones, zones are contained by compartments). Locations are described using x, y, and z co-ordinates (or length, width, and height).  

## Device

A device refers to any physical mechanism that can either monitor or control the growing environment (lights, pumps, heaters, humidifiers, etc).  

In the example, every device is related to a zone and a location within that zone. It should be able to report these relationships along with its own unique ID.  

## Sensor

A sensor refers to any device that is gathering data about the growing environment (light, air, water, nutrients, and so on).  

## Controller

A controller refers to any device that can affect the growing environment (light fixtures, nutrient dosers, heaters, humidifiers, and so on).  

# Endpoint Structure

The detailed endpoint structure is outside the scope of this document because it needs to make sense for the overall architecture of the implementation. However, there are a few standards that need to be considered when it comes to endpoint design.  


**Example**

GET https://www.googleapis.com/books/v1/volumes/zyTCAlFPjgYC?key=yourAPIKey

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
