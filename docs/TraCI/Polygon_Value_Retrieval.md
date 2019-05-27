---
title: TraCI Polygon Value Retrieval
permalink: /TraCI/Polygon_Value_Retrieval/
---

Command 0xa8: Get Polygon Variable
----------------------------------

|          |            |
|:--------:|:----------:|
|   ubyte  |   string   |
| Variable | Polygon ID |

Asks for the value of a certain variable of the named polygon.

The following variable values can be retrieved, the type of the return value is also shown in the table.

| Variable       | ValueType               | Description                                                             | [Python Method](/TraCI/Interfacing_TraCI_from_Python "wikilink")                              |
|----------------|-------------------------|-------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| id list (0x00) | stringList              | Returns a list of ids of all polygons (the given polygon ID is ignored) | [getIDList](http://www.sumo.dlr.de/daily/pydoc/traci._polygon.html#PolygonDomain-getIDList)   |
| count (0x01)   | int                     | Returns the number of polygons (the given polygon ID is ignored)        | [getIDCount](http://www.sumo.dlr.de/daily/pydoc/traci._polygon.html#PolygonDomain-getIDCount) |
| type (0x4f)    | string                  | Returns the (abstract) type of the polygon                              | [getType](http://www.sumo.dlr.de/daily/pydoc/traci._polygon.html#PolygonDomain-getType)       |
| color (0x45)   | ubyte,ubyte,ubyte,ubyte | Returns the color of this polygon (rgba)                                | [getColor](http://www.sumo.dlr.de/daily/pydoc/traci._polygon.html#PolygonDomain-getColor)     |
| shape (0x4e)   | 2D-polygon              | Returns the shape (list of 2D-positions) of this polygon                | [getShape](http://www.sumo.dlr.de/daily/pydoc/traci._polygon.html#PolygonDomain-getShape)     |
| filled (0x55)  | ubyte                   | Returns whether this polygon is filled (1) or not (0)                   | [getFilled](http://www.sumo.dlr.de/daily/pydoc/traci._polygon.html#PolygonDomain-getFilled)   |
||

### Response 0xb8: Polygon Variable

|          |            |                             |                  |
|:--------:|:----------:|:---------------------------:|:----------------:|
|   ubyte  |   string   |            ubyte            |   <return_type>  |
| Variable | Polygon ID | Return type of the variable | <VARIABLE_VALUE> |

The respond to a **“Command Get Polygon Variable”**.