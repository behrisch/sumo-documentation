---
layout: post
title: Simulation GenericParameters
permalink: /Simulation/GenericParameters/
---

Generic parameters allow an arbitrary mapping of string keys to string values. They can be used for user-defined data storage but some key/value pairs also affect the simulation.

The following objects support the definition of custom parameters in their XML definitions:

-   Edge
-   Lane
-   Person
-   Vehicle
-   VehicleType
-   PoI
-   Polygon
-   Route
-   TrafficLight

Parameters support the following functionality

-   reading and writing [via TraCI](/Traci/GenericParameters "wikilink").
-   customizing the functionality of [actuated traffic lights](/Simulation/Traffic_Lights#Additional_Parameters "wikilink")
-   configuring vehicle types for use with the [electric vehicle model](/Models/Electric "wikilink")
-   [setting up devices on a per-vehicle basis](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Devices "wikilink")

Parameters are always defined as child elements of the respective object:

`   `<vehicle id="v0" route="route0" depart="0">
`       `<param key="answer to everything" value="42"/>
`   `</vehicle>