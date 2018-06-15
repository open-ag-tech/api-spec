# Purpose

To provide a standard layout for the OpenAg structure YAML.
 
# Scope

Defining the structure's nodes, their attributes, and their subattributes.

#Nodes

```YAML
Nodes:
  Company:
    Required:
      ID: String
      Name: String
  Facility:
    Required:
      ID: String
    Optional:
      Name: String
      Address: String
      City: String
      State: String
      ZIP: String
      Size: Integer, Square Meters
      Length: Decimal, Meters
      Width: Decimal, Meters
      Height: Decimal, Meters
  Zone:
    Required:
      ID: String
      Type: [Compartment, Rack, Table, Level, Tray, AirZone, IrrZone, Row, Column]
    Optional:
      Size: Decimal, Square Meters
      Length: Decimal, Meters
      Width: Decimal, Meters
      Height: Decimal, Meters
      Location: Array, floor-plan bottom (Z) of top-left (X-Y) corner to bottom (Z) of top-left(X-Y) corner, meters #Zones will not always be on the floor. A zone (like a level on a Rack) might be 2 meters tall but 1.5 meters off the ground. The height should be 2 meters and the Z axis should be 1.5.
      Crop: String
      Variety: String
      CropStage: String
  Device:
    Required:
      ID: String
      Type: [Controller,Sensor]
      Domain: [Air,Light,Water,TBD] #We'll need to better define these
    Optional:
      Location: Array, floor-plan bottom  of top-left corner to bottom of top-left corner, meters
      Delay: Decimal, seconds #Expect a response after x seconds
      Control: [Direct,Indirect,RESTful] #Direct control means cutting power to the device. Indirect control means cutting power to a control voltage line. RESTful means a smart device capable of understanding an OpenAg API call.
      Make: String
      Model: String
      Version: String
      Power: #Device power, not control power
        Voltage: Integer #maxvoltage, when variable.
        AC: T/F #True is AC, False is DC
        Current: Integer #Amperes or VAC, Depending. Load current
        Inrush: Integer #Amperes or VAC
        Phase: Integer     
  Contact:
    Required:
      URI: String #Protocol:Address
      ControlType: [Binary, Digital, Analog]
    Optional:
      Name: String
      Quantity: Integer, Default 1
      Power: #control power, not device power. A device may draw 15 amps at 110 VAC but have contact/control power of milliamps at 24VAC
          voltage: Integer #max voltage, when variable.
          AC: T/F #True is AC, False is DC
          Current: Integer #Amperes or VAC, Depending. Load current
          Inrush: Integer #Amperes or VAC
          Phase: Integer
          
          
          
          
      