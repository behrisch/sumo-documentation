---
title: Simulation VehicleInsertion
permalink: /Simulation/VehicleInsertion/
---

__FORCETOC__

Loading
=======

Vehicles are either loaded [from XML inputs](/SUMO_User_Documentation#Demand_Modelling "wikilink") or [added at runtime via TraCI](/TraCI "wikilink"). When loading from XML, not all vehicles are loaded at once. Instead, vehicles are loaded in chunks, the size of which can be configured with the option . This is done to conserve memory when performing long simulations.

Once vehicles are loaded they can be accessed and manipulated via TraCI (to some degree). Using the functions 'move to' or 'move to XY' they can even be forcefully inserted into the network.

Insertion (Departure)
=====================

In order for a vehicle to be inserted into the road network, some necessary constraints must be fulfilled:

-   The vehicle (from its rear to its front position + *minGap*) must not intersect with other vehicles (including their *minGap*
-   The vehicle must be at a safe distance to any leader vehicles according to its *carFollowModel*
-   Any follower vehicles must be at a safe distance according to their *carFollowModel*
-   The vehicle must be able to brake for any upcoming non-prioritized intersections along its route
-   The vehicle must be able to brake for any scheduled stops along its route

If a vehicle cannot be inserted due to any of the above reasons it's insertion is delayed (see below). This *departDelay* is recorded in the [tripinfo-output](/Simulation/Output/TripInfo "wikilink") and can also be inspected in [SUMO-GUI](/SUMO-GUI "wikilink") via the vehicle parameter dialog.

The precise nature of insertion in regard to position, speed and depart time depend on [many parameters](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Vehicles_and_Routes "wikilink") as well as on the current state of the road network.

Delayed Departure
-----------------

If there is insufficient space for inserting the vehicle at it's designated departure time, that vehicle is put into an insertion queue and insertion is repeatedly attempted in subsequent simulation steps. If the option is used, vehicles are discarded if they could not be inserted after the specified in seconds.

There are two methods for inserting vehicles into the simulation:

1.  try to insert every vehicle in every simulation step
2.  for every edge with vehicles to insert, abort trying to insert vehicles after one of the vehicles could not be inserted

In an uncongested networks these methods behave similar but in a congested network with lots of vehicles which cannot be inserted variant 2) is much faster. In older version of sumo 1) was the default and one could switch to 2) using the option Since version 0.18.0, variant 2) is the default and one may switch to 1) using the option .

Investigating insertion delay
-----------------------------

Using [SUMO-GUI](/SUMO-GUI "wikilink") several options exist for showing insertion delay:

-   Color vehicles *by insertion delay*
-   Color Streets *by insertion backlog*
-   Opening Vehicle statistics lists the number of *insertion-backloged vehicles* for the whole network.

Global options that affect Departure
------------------------------------

-
    randomly delays departure time for all vehicles

-
    limits the total amount of vehicles that may exist in the networ. Setting this may cause delayed insertion

-
    removes vehicles from the insertion queue after a set amount of time

-
    tries to insert all vehicles that are insertion-delayed on each edge. By default, insertion on an edge stops after the first failure in each time step

Miscellaneous
=============

-   For tips on how to achieve high insertion flows see [the FAQ](/FAQ#How_do_I_get_high_flows.2Fvehicle_densities.3F "wikilink")
-   Vehicles can also be inserted through the use of [calibrators](/Simulation/Calibrator "wikilink")
-   Vehicle rerouting may be triggered even before departure [when using device.rerouting](/Demand/Automatic_Routing "wikilink")
-   The departure edge can be determined at run-time when using [Traffic Assignment Zones (TAZ)](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Traffic_assignement_zones_.28TAZ.29 "wikilink")
