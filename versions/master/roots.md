# Purpose

This specification is intended to define a standardized way of communicating with climate control systems for real-time monitoring and control of root systems and to allow data collection between systems and / or peripheral devices.

# Scope

The scope of this document is limited to providing a payload structure and endpoint type definitions to allow basic control and data acquisition. The addition of product specific features is left to the implementer, but to be in compliance the product must support the basic set of features specified below.

# Definitions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

# Endpoints
## Sensors
### URLS
### Measurements
| Data point | Description                                                              | Unit    |
| ---------- | ------------------------------------------------------------------------ | ------- |
| water      | The amount of the water surrounding the roots (aquaponics & hydroponics) | %       |
| light      | The level of all spectrums of light                                      | µmoles  |
| temp       | The temperature of the water / air around the roots                      | celsius |
| humidity   | The level of humidity around the roots (for airponics)                   | %       |
| oxygen     | The amount of oxygen dissolved in the water** around the roots           | ppm     |
| ec         | The electrical conductivity of the water** around the roots              | Ds / m  |
| ph         | The alkalinity of the water** around the roots                           | n/a     |

**NOTE:** for airponics, water levels would be measured from the moisture in the air around the roots
