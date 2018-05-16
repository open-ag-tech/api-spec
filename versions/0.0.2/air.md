# Purpose

This specification is intended to define a standardized way of communicating with climate control systems for real-time monitoring and control of air quality and to allow data collection between control systems and / or peripheral devices.

# Scope

The scope of this document is limited to providing a payload structure and endpoint type definitions to allow basic control and data acquisition. The addition of product specific features is left to the implementer, but to be in compliance the product must support the basic set of features specified below.

# Definitions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

# Endpoints
## Sensors
### URLS
### Measurements
| Data point | Description                      | Unit    |
| ---------- | -------------------------------- | ------- |
| temp       | The temperature of the air       | celsius |
| humidity   | The level of humidity in the air | %       |
| co2        | The level of CO2 in the air      | ppm     |
| airflow    | The speed of the airflow         | m3/s    |