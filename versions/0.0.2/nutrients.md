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
| Data point | Description                   | Unit |
| ---------- | ----------------------------- | ---- |
| nitrogen   | The amount of nitrogen (N)    | ppm  |
| phosphorus | The amount of phosphorus (P)  | ppm  |
| potassium  | The amount of potassium (K)   | ppm  |
| sulphur    | The amount of sulfur (S)      | ppm  |
| calcium    | The amount of calcium (Ca)    | ppm  |
| magnesium  | The amount of magnesium (Mg)  | ppm  |
| iron       | The amount of iron (Fe)       | ppm  |
| manganese  | The amount of manganese (Mg)  | ppm  |
| boron      | The amount of boron (B)       | ppm  |
| copper     | The amount of copper (Cu)     | ppm  |
| zinc       | The amount of zinc (Zn)       | ppm  |
| molybdenum | The amount of molybdenum (Mo) | ppm  |
| ammonium   | The amount of ammonium (NH4+) | ppm  |
