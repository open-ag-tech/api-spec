# Purpose

This specification is intended to define a standardized way of communicating with soil systems for real-time monitoring and control and to allow data collection between control systems and / or peripheral devices.

# Scope

The scope of this document is limited to providing a payload structure and endpoint type definitions to allow basic control and data acquisition. The addition of product specific features is left to the implementer, but to be in compliance the product must support the basic set of features specified below.

# Definitions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

# Endpoints
## Sensors
### URLS
### Measurements
| Data point    | Description                                                             | Unit       |
| ------------- | ----------------------------------------------------------------------- | ---------- |
| heatflow      | The amount of heat that transfers from one point in the soil to another | watts / m2 |
| h2o-retention | The rate at which water dissipates from the soil                        | ???        |
| soil-temp     | The temperature of the soil                                             | celsius    |
| humidity      | The amount of humidity in the soil                                      | %          |
| oxygen        | The amount of oxygen dissolved in the soil                              | %          |
| ec            | The electrical conductivity of the soil                                 | Ds / m     |
| ph            | The alkalinity of the soil                                              | n/a        |
