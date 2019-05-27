---
title: Simulation ParkingArea
permalink: /Simulation/ParkingArea/
---

__FORCETOC__

Parking Areas
=============

Areas for parking outside the road network (either road-side parking or car parks) can be defined using the element. This accomplishes the following purposes:

-   arbitrary parking positions and angles can be defined to visualize fishbone or parallel parking
-   parking space outside the road network can be limited to a set capacity
-   automatic rerouting to an alternative parking area can be triggered whenever a parking area becomes full

Definition
==========

A road-side parkingArea is defined as in the following:

<parkingArea id="ParkAreaA" lane="a_0" startPos="200" endPos="250" roadsideCapacity="5" angle="45" length="30"/>

Additionally, individual parking spaces can be defined:

<parkingArea id="ParkAreaB" lane="b_0" startPos="240" endPos="260" roadsideCapacity="0" width="5" length="10" angle="30">
`    `<space x="853" y="623"/>
`    `<space x="863" y="618"/>
`    `<space x="873" y="613"/>
`    `<space x="883" y="608"/>
`    `<space x="893" y="603"/>
`    `<space x="848" y="611" width="4" length="8" angle="120"/>
`    `<space x="858" y="606" width="4" length="8" angle="120"/>
`    `<space x="868" y="601" width="4" length="8" angle="120"/>
`    `<space x="878" y="596" width="4" length="8" angle="120"/>
`    `<space x="888" y="591" width="4" length="8" angle="120"/>
</parkingArea>

The total capacity of a parking area is given by the sum of its *roadsideCapacity* and the number of its elements.

The parkingArea supports the following attributes:

| Attribute Name   | Value Type     | Value Range                                                                                     | Default                                | Description                                                                                                                |
|------------------|----------------|-------------------------------------------------------------------------------------------------|----------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| **id**           | string         | id                                                                                              |                                        | The name of the parking area; must be unique                                                                               |
| **lane**         | string         | valid lane id                                                                                   |                                        | The name of the lane the parking area shall be located at                                                                  |
| **startPos**     | float          | -lane.length &lt; x &lt; lane.length (negative values count backwards from the end of the lane) | 0                                      | The begin position on the lane (the lower position on the lane) in meters                                                  |
| endPos           | float          | -lane.length &lt; x &lt; lane.length (negative values count backwards from the end of the lane) | lane.length                            | The end position on the lane (the higher position on the lane) in meters, must be larger than *startPos* by more than 0.1m |
| friendlyPos      | bool           | *true,false*                                                                                    | *false*                                | whether invalid stop positions should be corrected automatically (default *false*)                                         |
| name             | string         | simple String                                                                                   |                                        | Arbitrary text to describe the parking area. This is only used for visualization purposes.                                 |
| roadsideCapacity | int            | non-negative                                                                                    | 0                                      | The number of parking spaces for road-side parking                                                                         |
| width            | float          | positive                                                                                        | 3.2                                    | The width of the road-side parking spaces                                                                                  |
| length           | float          | positive                                                                                        | (endPos - startPos) / roadsideCapacity | The length of the road-side parking spaces                                                                                 |
| angle            | float (degree) |                                                                                                 | 0                                      | The angle of the road-side parking spaces relative to the lane angle, positive means clockwise                             |

Custom parking spaces
---------------------

The space element supports the following attributes:

| Attribute Name | Value Type     | Value Range | Default                                                                  | Description                                     |
|----------------|----------------|-------------|--------------------------------------------------------------------------|-------------------------------------------------|
| **x**          | float          |             |                                                                          | The x-position in meters of the parking vehicle |
| **y**          | float          |             |                                                                          | The y-position in meters of the parking vehicle |
| z              | float          |             | 0                                                                        | The z-position in meters of the parking vehicle |
| width          | float          |             | width value of the parent parking area                                   | The width of the parking space                  |
| length         | float          |             | length value of the parent parking area                                  | The length of the parking space                 |
| angle          | float (degree) |             | absolute angle of the parent parking area (lane angle + angle attribute) | Absolute angle of the parking space             |
||

Letting Vehicles stop at a parking area
=======================================

The declare a vehicle that stops at a parkingPlace, a -definition must be part of the vehicle or it's route:


        <vehicle id="0" depart="0">
            <route edges="e1 e2 e3"/>
            <stop parkingArea="pa0" duration="20"/>
        </vehicle>

What is defined here is a vehicle named “0” that stops as at parkingArea “pa0”. Note, that the lane of that parking area must belong to one of the edges “e1, e2, e3” of the vehicles route.

For a complete list of attributes for the “stop”-element of a vehicle see [Definition_of_Vehicles,_Vehicle_Types,_and_Routes\#Stops](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Stops "wikilink").

If a vehicle reaches a parkingArea that is filled to capacity it must wait on the road until a space becomes available or [reroute to a new parking area](/Simulation/Rerouter#Rerouting_to_an_alternative_Parking_Area "wikilink").

TraCI
=====

Some information regarding parking areas can be accessed directly using [traci.simulation.getParameter() calls](/TraCI/Simulation_Value_Retrieval#Generic_Parameter_Retrieval_0x7e "wikilink").

-   **parkingArea.capacity**: total number of parking spaces (roadsideCapacity + number of elements)
-   **parkingArea.occupancy**: number of vehicles parking at this parking area
