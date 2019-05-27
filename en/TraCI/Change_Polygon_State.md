---
layout: post
title: TraCI Change Polygon State
permalink: /TraCI/Change_Polygon_State/
---

Command 0xc8: Change Polygon State
==================================

|          |            |                   |              |
|:--------:|:----------:|:-----------------:|:------------:|
|   ubyte  |   string   |       ubyte       | <value_type> |
| Variable | Polygon ID | Type of the value |   New Value  |

Changes the state of a polygon. Because it is possible to change different values of a polygon, the number of parameter to supply and their types differ between commands. The following values can be changed, the parameter which must be given are also shown in the table.

| Variable      | ValueType                       | Description                                                                                                  | [Python Method](/TraCI/Interfacing_TraCI_from_Python "wikilink")                            |
|---------------|---------------------------------|--------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| type (0x4f)   | string                          | Sets the polygon's type to the given value                                                                   | [setType](http://www.sumo.dlr.de/daily/pydoc/traci._polygon.html#PolygonDomain-setType)     |
| color (0x45)  | color (ubyte,ubyte,ubyte,ubyte) | Sets the polygon's color to the given value (r,g,b,a) - please note that a(lpha) = 0 means fully transparent | [setColor](http://www.sumo.dlr.de/daily/pydoc/traci._polygon.html#PolygonDomain-setColor)   |
| shape (0x4e)  | 2D-polygon                      | Sets the polygon's shape to the given value                                                                  | [setShape](http://www.sumo.dlr.de/daily/pydoc/traci._polygon.html#PolygonDomain-setShape)   |
| filled (0x55) | ubyte                           | Marks that the polygon shall be filled if the value is !=0.                                                  | [setFilled](http://www.sumo.dlr.de/daily/pydoc/traci._polygon.html#PolygonDomain-setFilled) |
| ADD (0x80)    | Polygon-definition, see below   | Adds the defined Polygon                                                                                     | [add](http://www.sumo.dlr.de/daily/pydoc/traci._polygon.html#PolygonDomain-add)             |
| REMOVE (0x81) | int (layer), see below          | Removes the defined Polygon                                                                                  | [remove](http://www.sumo.dlr.de/daily/pydoc/traci._polygon.html#PolygonDomain-remove)       |
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

### shape (0x42)

|                      |                  |                 |                 |     |                   |                   |
|:--------------------:|:----------------:|:---------------:|:---------------:|:---:|:-----------------:|:-----------------:|
|         ubyte        |       ubyte      |      double     |      double     | ... |       double      |       double      |
| value type *polygon* | entry number (n) | x-coordinate\#0 | y-ccordinate\#0 | ... | x-coordinate\#n-1 | y-coordinate\#n-1 |

### filled (0x55)

|                    |              |
|:------------------:|:------------:|
|        ubyte       |     ubyte    |
| value type *ubyte* | filled (!=0) |

### ADD (0x80)

|                       |                 |                     |           |                    |       |                    |        |                  |       |                    |       |
|:---------------------:|:---------------:|:-------------------:|:---------:|:------------------:|:-----:|:------------------:|:------:|:----------------:|:-----:|:------------------:|:-----:|
|         ubyte         |       int       |        ubyte        |   string  |        ubyte       | color |        ubyte       |  ubyte |       ubyte      |  int  |        ubyte       | shape |
| value type *compound* | item number = 5 | value type *string* | type name | value type *color* | color | value type *ubyte* | filled | value type *int* | layer | value type *shape* | shape |

If the polygon could not been added because another one with the same ID already exists within the layer, an error message is generated.

### REMOVE (0x81)

|                  |       |
|:----------------:|:-----:|
|       ubyte      |  int  |
| value type *int* | layer |

If the named polygon can not be found in the given layer, all polygons with the given ID are removed (from all layers). If no polygon with the given ID could be found, an error message is generated.