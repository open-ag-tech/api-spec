# Purpose

To provide a standard layout for the OpenAg structure YAML.

# Scope

Defining the structure's nodes, their attributes, and their subattributes.

#Nodes

```YAML

openapi: "3.0.0"
info:
  version: 1.0.0
  title: OpenAg Farms
  license:
    name: MIT
servers:
  - url: http:www.openagfarms.com
paths:
  /facilities:
    get:
      summary: List all facilities and their contents
    operationId: listFacilities
      tags:
        - facilities
      parameters:
        - name: limit
          in: query
          description: How many items to return at one time (max 100)
          required: false
          schema:
            type: integer
            format: int32
      responses:
        '200':
          description: A paged array of facilities
          headers:
            x-next:
              description: A link to the next page of responses
              schema:
                type: string
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Facilities"
        default:
          description: unexpected error
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Error"
    post:
      summary: Create a facility
      operationId: create
      tags:
        - facilities
      responses:
        '201':
          description: Null response
        default:
          description: unexpected error
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Error"
components:
  schemas:
    Device:
      required:
        - id
        - name
        - kind
        - domain
      properties:
        id:
          type: string
        name:
          type: string
        kind:
          enum: [Controller, Sensor]
        domain:
          enum: [Air, Light, Water]
        location:
          type: array
    Zone:
      required:
        - id
        - name
        - kind
      properties:
        id:
           type: string
        name:
          type: string
        kind:
          enum: [Compartment, Rack, Table, Level, Tray, AirZone, IrrZone, Row, Column]
        Device:
          object:
          items:
            $ref: "#/components/schemas/Device"
    Facility:
      required:
        - id
        - zone
      properties:
        id:
          type: string
        Zone:
          type: object
          items:
            $ref: "#components/schemas/Zone"
        name:
          type: string
        size:
          type: integer
          format: int32
        height:
          type: integer
          format: int32
        width:
          type: integer
          format: int32
        length:
          type: integer
          format: int32
    Facilities:
      type: array
      items:
        $ref: "#/components/schemas/Facility"
    Error:
      required:
        - code
        - message
      properties:
        code:
          type: integer
          format: int32
        message:
          type: string