---
layout: post
title: TraCI Person Value Retrieval
permalink: /TraCI/Person_Value_Retrieval/
---

__TOC__

Command 0xae: Get Person Variable
---------------------------------

|          |           |
|:--------:|:---------:|
|   ubyte  |   string  |
| Variable | Person ID |

Asks for the value of a certain variable of the named person. The value returned is the state of the asked variable/value within the last simulation step. In the case the person is loaded, but outside the network - due not being yet inserted into the network or being teleported within the current time step - a default “error” value is returned.

The following variable values can be retrieved, the type of the return value is also shown in the table.

| Variable                | ValueType               | Description                                                                                                                                                    | [Python Method](/TraCI/Interfacing_TraCI_from_Python "wikilink")                                      |
|-------------------------|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| id list (0x00)          | stringList              | Returns a list of ids of all persons currently running within the scenario (the given person ID is ignored)                                                    | [getIDList](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getIDList)             |
| count (0x01)            | int                     | Returns the number of persons currently running within the scenario (the given person ID is ignored)                                                           | [getIDCount](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getIDCount)           |
| speed (0x40)            | double                  | Returns the speed of the named person within the last step \[m/s\]; error value: -1001                                                                         | [getSpeed](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getSpeed)               |
| position (0x42)         | position                | Returns the position(two doubles) of the named person within the last step \[m,m\]; error value: \[-2^30, -2^30\].                                             | [getPosition](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getPosition)         |
| position 3D (0x39)      | position                | Returns the 3D-position(three doubles) of the named vehicle (center of the front bumper) within the last step \[m,m,m\]; error value: \[-2^30, -2^30, -2^30\]. | [getPosition3D](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getPosition3D)     |
| angle (0x43)            | double                  | Returns the angle of the named person within the last step \[°\]; error value: -1001                                                                           | [getAngle](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getAngle)               |
| road id (0x50)          | string                  | Returns the id of the edge the named person was at within the last step; error value: ""                                                                       | [getRoadID](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getRoadID)             |
| type id (0x4f)          | string                  | Returns the id of the type of the named person                                                                                                                 | [getTypeID](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getTypeID)             |
| color (0x45)            | ubyte,ubyte,ubyte,ubyte | Returns the person's color (RGBA).                                                                                                                             | [getColor](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getColor)               |
| edge position (0x56)    | double                  | The position of the person along the edge (in \[m\]); error value: -1001                                                                                       | [getLanePosition](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getLanePosition) |
| length (0x44)           | double                  | Returns the length of the persons \[m\]                                                                                                                        | [getLength](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getLength)             |
| minGap (0x4c)           | double                  | Returns the offset (gap to front person if halting) of this person \[m\]                                                                                       | [getMinGap](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getMinGap)             |
| width (0x4d)            | double                  | Returns the width of this person \[m\]                                                                                                                         | [getWidth](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getWidth)               |
| waiting time (0x7a)     | double                  | Returns the waiting time \[s\]                                                                                                                                 | [getWaitingTime](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getWaitingTime)   |
| next edge (0xc1)        | string                  | Returns the next edge on the persons route while it is walking. If there is no further edge or the person is in another stage, returns the empty string.       | [getNextEdge](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getNextEdge)         |
| remaining stages (0xc2) | int                     | Returns the number of remaining stages for the given person including the current stage.                                                                       | [getRemainingStages](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getStage)     |
| vehicle (0xc3)          | string                  | Returns the id of the vehicle if the person is in stage driving and has entered a vehicle.                                                                     | [getVehicle](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getVehicle)           |
||

Response 0xb4: Person Variable
------------------------------

|          |           |                             |                  |
|:--------:|:---------:|:---------------------------:|:----------------:|
|   ubyte  |   string  |            ubyte            |   <return_type>  |
| Variable | Person ID | Return type of the variable | <VARIABLE_VALUE> |

The respond to a **“Command Get Person Variable”**.

Extended retrieval messages
---------------------------

Some further messages require additional parameters.

| Variable     | Request ValueType      | Response ValueType | Description                                                                                                                                                                                                                                                    | [Python Method](/TraCI/Interfacing_TraCI_from_Python "wikilink")                        |
|--------------|------------------------|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| stage (0xc0) | next stage index (int) | int                | Returns the stage type of nth next stage. Index 0 retrieves the value for the current stage. The given index must be lower than the value of 'remaining stages'. The return values have the following meaning: 0:driving, 1:waiting, 2:walking, 3:not departed | [getStage](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getStage) |
| edges (0x54) | next stage index (int) | stringList         | Returns the edges of the nth next stage. Index 0 retrieves the value for the current stage. The given index must be lower than the value of 'remaining stages'. For driving stages only origin and destination edge are returned.                              | [getEdges](http://www.sumo.dlr.de/daily/pydoc/traci._person.html#PersonDomain-getEdges) |
||

