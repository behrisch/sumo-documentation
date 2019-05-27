---
title: TraCI POI Value Retrieval
permalink: /TraCI/POI_Value_Retrieval/
---

Command 0xa7: Get PoI Variable
------------------------------

|          |        |
|:--------:|:------:|
|   ubyte  | string |
| Variable | PoI ID |

Asks for the value of a certain variable of the named poi.

The following variable values can be retrieved, the type of the return value is also shown in the table.

| Variable        | ValueType               | Description                                                    | [Python Method](/TraCI/Interfacing_TraCI_from_Python "wikilink")                        |
|-----------------|-------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| id list (0x00)  | stringList              | Returns a list of ids of all poi (the given poi ID is ignored) | [getIDList](http://www.sumo.dlr.de/daily/pydoc/traci._poi.html#PoiDomain-getIDList)     |
| count (0x01)    | int                     | Returns the number of pois (the given poi ID is ignored)       | [getIDCount](http://www.sumo.dlr.de/daily/pydoc/traci._poi.html#PoiDomain-getIDCount)   |
| type (0x4f)     | string                  | Returns the (abstract) type of the poi                         | [getType](http://www.sumo.dlr.de/daily/pydoc/traci._poi.html#PoiDomain-getType)         |
| color (0x45)    | ubyte,ubyte,ubyte,ubyte | Returns the color of this poi (rgba)                           | [getColor](http://www.sumo.dlr.de/daily/pydoc/traci._poi.html#PoiDomain-getColor)       |
| position (0x42) | 2D-position             | Returns the position of this poi                               | [getPosition](http://www.sumo.dlr.de/daily/pydoc/traci._poi.html#PoiDomain-getPosition) |
||

### Response 0xb7: PoI Variable

|          |        |                             |                  |
|:--------:|:------:|:---------------------------:|:----------------:|
|   ubyte  | string |            ubyte            |   <return_type>  |
| Variable | PoI ID | Return type of the variable | <VARIABLE_VALUE> |

The respond to a **“Command Get PoI Variable”**.