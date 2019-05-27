---
layout: post
title: TraCI Change PoI State
permalink: /TraCI/Change_PoI_State/
---

Command 0xc7: Change PoI State
==============================

|          |        |                   |              |
|:--------:|:------:|:-----------------:|:------------:|
|   ubyte  | string |       ubyte       | <value_type> |
| Variable | PoI ID | Type of the value |   New Value  |

Changes the state of a point-of-interest. Because it is possible to change different values of a PoI, the number of parameter to supply and their types differ between commands. The following values can be changed, the parameter which must be given are also shown in the table.

| Variable        | ValueType                       | Description                                                                                              | [Python Method](/TraCI/Interfacing_TraCI_from_Python "wikilink")                        |
|-----------------|---------------------------------|----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| type (0x4f)     | string                          | Sets the PoI's type to the given value                                                                   | [setType](http://www.sumo.dlr.de/daily/pydoc/traci._poi.html#PoiDomain-setType)         |
| color (0x45)    | color (ubyte,ubyte,ubyte,ubyte) | Sets the PoI's color to the given value (r,g,b,a) - please note that a(lpha) = 0 means fully transparent | [setColor](http://www.sumo.dlr.de/daily/pydoc/traci._poi.html#PoiDomain-setColor)       |
| position (0x42) | Position2D (double, double)     | Sets the PoI's position to the given value                                                               | [setPosition](http://www.sumo.dlr.de/daily/pydoc/traci._poi.html#PoiDomain-setPosition) |
| ADD (0x80)      | PoI-definition, see below       | Adds the defined PoI                                                                                     | [add](http://www.sumo.dlr.de/daily/pydoc/traci._poi.html#PoiDomain-add)                 |
| REMOVE (0x81)   | int (layer), see below          | Removes the defined PoI                                                                                  | [remove](http://www.sumo.dlr.de/daily/pydoc/traci._poi.html#PoiDomain-remove)           |
||

The message contents are as following:

### type (0x4f)

|                     |               |
|:-------------------:|:-------------:|
|        ubyte        |     string    |
| value type *string* | New Type Name |

### color (0x45)

|                    |       |       |       |       |
|:------------------:|:-----:|:-----:|:-----:|:-----:|
|        ubyte       | ubyte | ubyte | ubyte | ubyte |
| value type *color* |  red  | green |  blue | alpha |

### position (0x42)

|                         |              |              |
|:-----------------------:|:------------:|:------------:|
|          ubyte          |    double    |    double    |
| value type *position2D* | x-coordinate | y-ccordinate |

### ADD (0x80)

|                       |                 |                     |           |                    |       |                  |       |                         |          |
|:---------------------:|:---------------:|:-------------------:|:---------:|:------------------:|:-----:|:----------------:|:-----:|:-----------------------:|:--------:|
|         ubyte         |       int       |        ubyte        |   string  |        ubyte       | color |       ubyte      |  int  |          ubyte          | position |
| value type *compound* | item number = 4 | value type *string* | type name | value type *color* | color | value type *int* | layer | value type *position2D* | position |

If the PoI could not been added because another one with the same ID already exists within the layer, an error message is generated.

### REMOVE (0x81)

|                  |       |
|:----------------:|:-----:|
|       ubyte      |  int  |
| value type *int* | layer |

If the named PoI can not be found in the given layer, all PoIs with the given ID are removed (from all layers). If no PoI with the given ID could be found, an error message is generated.