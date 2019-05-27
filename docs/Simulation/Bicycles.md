---
layout: post
title: Simulation Bicycles
permalink: /Simulation/Bicycles/
---

Bicycle Simulation
==================

This page describes simulations of bicycles in SUMO. To build an intermodal simulation scenario with bicycles, additional steps have to be take in comparison to a plain vehicular simulation.

Approaches to bicycle modelling
===============================

Currently, no exclusive movement model for bicycles is implemented. Existing models need to be re-purposed

Bicycles as slow vehicles
-------------------------

In this case, vehicles are specified as vehicles with the appropriate type:

<vType id="bike" vClass="bicycle"/>
<vehicle type="bike" .../>

Note, that that the along with [sensible default parameters](/Vehicle_Type_Parameter_Defaults "wikilink") are automatically used when specifying . By adapating [vType-parameters for acceleration,deceleration,maximumSpeed,etc..](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Vehicle_Types "wikilink") different cyclist types can be modelled.

### Problems and workarounds

-   Turning left by crossing twice does not work. Extra edges need to be added to accommodate these trajectories.
-   No bi-directional movements on bicycle lanes
-   No shared space for bicycles and pedestrians
-   No overtaking by vehicles on a single-lane road. This can be fixed by using the [Sublane Model](/Simulation/SublaneModel "wikilink").
-   The intersection model has no special adaptations for bicycles. This results in unrealistic (large) safety gaps when bicycles are approaching a large priority intersection from a prioritized road
-   The road speed limit is not meaningful for bicycles. To [model a speed distribution for bicycles with a single vehicle type](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Speed_Distributions "wikilink"), a speed limit corresponding to the median speed of the bicycles should be set for the cycling lanes.

One way for overcoming most of these problems is to control bicycle movements at intersections with an [external control script](/TraCI "wikilink"). This approach is described in [Integration of an external bicycle model in SUMO, Heather Twaddle 2016](https://www.researchgate.net/publication/302909195_Integration_of_an_External_Bicycle_Model_in_SUMO).

Bicyles as fast pedestrians
---------------------------

In this case, persons walking at high speed are used.

### Problems and workarounds

-   No support for proper visualization
-   Movement model is not validated

Building a network for bicycle simulation
=========================================

Automatic import
----------------

The import of bicycle lanes from OpenStreetMap is supported since version 0.24.0. To use this, [an appropriate typemap](/Networks/Import/OpenStreetMap#Recommended_Typemaps "wikilink") must be loaded.

### Explicity specification

Bike lanes may be defined explicitly in plain XML input when describing [edges (plain.edg.xml)](/Networks/Building_Networks_from_own_XML-descriptions#Lane-specific_Definitions "wikilink"). This is done by defining an additional lane which only permits the vClass “bicycle” and setting the appropriate width. In this case it is important to disallow bicycles on all other lanes. Also, any pre-exisiting connection definitions must be modified to account for the new sidewalk lane.

Notes on Right-of-Way rules
---------------------------

When using bicycle lanes in a network, right-turning vehicles must yield for straight-going bicycles. The intersection model supports these right-of-way rules and builds internal junctions where appropriate.

Likewise, left-turning bicycles one a bicycle lane (on the right side of the road) must yield to straight-going vehicles.