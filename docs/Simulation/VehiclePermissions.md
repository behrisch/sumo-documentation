---
layout: post
title: Simulation VehiclePermissions
permalink: /Simulation/VehiclePermissions/
---

__FORCETOC__

Introduction
============

SUMO allows modelling access restrictions via a predefined set of so-called vehicle classes. Each vehicle has a vehicle class and each simulation lane allows a set of vehicle classes. Vehicles may only drive on lanes that allows it's vehicle class.

This is useful for describing multi-modal traffic scenarios by distinguishing between passenger cars, bicycles, tram and pedestrians.

Vehicle definition
==================

The vehicle class of a vehicle is defined by first defining a [vehicle type](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Vehicle_Types "wikilink") with the appropriate [vehicle class](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Abstract_Vehicle_Class "wikilink") and then[assigning that type to the vehicle](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Vehicles_and_Routes "wikilink"). An example is given below:

    <routes>
       <vType id="myType" vClass="bus"/>

       <vehicle id="veh0" type="myType" depart="0">
          <route edges="a b c"/>
       </vehicle>
    </routes>

If no such definition is given, the vehicle class defaults to *passenger* (normal passenger cars). By setting the attribute, a set of [default type parameters](/Vehicle_Type_Parameter_Defaults "wikilink") is automatically assigned to better correspond to a typical vehicle of that class.

Network definition
==================

In a *.net.xml* file, each lane defines a set of permitted vehicle classes. This definition is either

-   taken from [custom input files](/Networks/Building_Networks_from_own_XML-descriptions#Edge_Descriptions "wikilink"). It possible to define permissions for edges or individual lanes. To simplify definition, either the permitted classes or the prohibited classes can be specified using the attributes .
-   set using the option
-   imported from an input source such as [OpenStreetMap](/Networks/Import/OpenStreetMap "wikilink") according to a [customizable heuristic](/Networks/Import/OpenStreetMap#Recommended_Typemaps "wikilink").
-   or set via [NETEDIT](/NETEDIT#Inspect "wikilink"). Convenience features exist [for adding bicycle lanes, bus lanes and sidewalks](/NETEDIT#Restricted_lanes "wikilink").

For visualizing access permissions, either [SUMO-GUI](/SUMO-GUI#Road_Access_Permissions "wikilink") or [NETEDIT](/NETEDIT#Correcting_road_access_permissions "wikilink") may be used.

Special cases
=============

The vehicle class *ignoring* may drive on any edge.

The vehicle class *pedestrian* should not be assigned to a vehicle. Instead, pedestrians should be modeled as [walking persons](/Simulation/Pedestrians "wikilink"). During network building, no direct connections between pedestrian-only lanes are built. Instead options for [building pedestrian intersections](/Simulation/Pedestrians#Building_a_network_for_pedestrian_simulation "wikilink") should be used.