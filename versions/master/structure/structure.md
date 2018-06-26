# Purpose

This structure is intended to facilitate machine understanding of the physical structure of a facility or facilities owned by a company. By providing a format for a single location for the storage of structure information, the potential for confusion created by multiple devices each attempting to describe their own environment is reduced. 

# Scope

This structure document will describe the devices, their contact points, and their logical and physical locations within the growing facilities of a particular company.

# Definitions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

# Structure Organization

Within a facility, all devices are to be organized within the following hierarchy. Each node within the hierarchy will have a set of attributes as defined within this document. 

![Common Concepts](https://www.lucidchart.com/publicSegments/view/b6b65937-424b-4538-b5ea-2bbb6f771d75/image.png)

## Company

A company refers to a single entity that owns and operates one or more facilities.

## Facility

A facility is a single physical site that contains one or more zone - e.g., a greenhouse or a warehouse. A company can own many facilities. Companies with centralized controls will want to use a single document to structure all of their facilities. Others might prefer to keep each facility's structure document separate.

## Zone

A zone identifies an area within a facility. Zones may be nested within zones to create any number of specific areas. For example, a facility might use nested zones to describe a compartment or room, a rack within that room, a level within a rack, and a tray within a level. 

## Device

A device refers to any physical mechanism that can either monitor or control the growing environment (lights, pumps, heaters, humidifiers, etc).  Devices must be located within a single parent zone.

## Contact

A contact is the point at which a device makes contact with the network or a controller. Each contact point must have a URI.