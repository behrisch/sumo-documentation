---
title: Simulation Intersections
permalink: /Simulation/Intersections/
---

The vehicle dynamics at intersection are governed by the intersection model described in [*Road Intersection Model in SUMO, Krajzewicz et al*](/http://elib.dlr.de/93669/1/LNCS_SUMOIntersections.pdf "wikilink"). Of course, the model in the latest revision may deviate somewhat due to the ongoing evolution of the model. This page gives an overview over the configuration options governing the intersection model.

Internal links
==============

The most important configuration aspect is whether the dynamics within an intersection shall be modelled or not. This is configured using the following options

[NETCONVERT](/NETCONVERT "wikilink")-option
--------------------------------------------

When set to **true**, the network will not contain *internal lanes*, that is lanes within an intersection. Instead, vehicles will *jump* across the intersection. To avoid a systematic shortening of route lengths, the length of all edges is set artificially to the length between junction centers without changing their appearance. When set to **false** (the default), The network will contain lanes within intersections on which vehicles will drive just as on normal lanes, albeit subject to some blocking constraints.

[SUMO](/SUMO "wikilink")-option
--------------------------------

Whenn set to **true**, lanes within intersections are ignored. This option is not needed when the network does not contain them in the first place. Note, that route lengths will be wrong when ignoring internal lanes in a network that includes them.

Waiting before the Intersection
===============================

Vehicles wait with a context dependent offset before the end of their lane where it meets the intersection. The exact position depends on several factors explained below.

Lane Shape
----------

Usually the lane ends exactly where the intersection shape starts. One way to customize the exact position for each lane is to [edit the intersection shape](/NETEDIT#Junction "wikilink"). An alternative method is to [set a custom endpoint for an edge](/NETEDIT#Specifying_the_complete_geometry_of_an_edge_including_endpoints "wikilink").

Antoher possibility is the set the *endOffset* attribute for either the or or element. This will shorten the edge/lane by a set amount.

Right-Of-Way
------------

Vehicles from a minor road wait exactly at the end of the lane in order to minimize the distance they have to cover when a suitable gap in traffic is found. Vehicles waiting at at a traffic light wait with an offset of 1m ahead of the lane end.

Vehicle Class
-------------

Waiting Within the Intersection
===============================

In some situations, drivers are permitted to wait within the intersection for a gap in foe traffic. Typical cases are left-turning vehicles from the prioritized direction that wait for oncoming traffic or right-turning vehicles that have to wait for straight-going pedestrians. In SUMO this is modeled with [internal junctions](/Networks/SUMO_Road_Networks#Internal_Junctions "wikilink"). An internal junction splits the internal lane in two parts. Upon reaching the intersection, drivers may enter the intersection and drive up to the end of the first part despite approaching foe vehicles. They are not permitted to enter the intersection if it is blocked by vehicles already on the intersection or if there is a red traffic light.

When building networks, [NETCONVERT](/NETCONVERT "wikilink") automatically recognizes common cases for waiting within the intersection and creates internal junctions as necessary. At intersections which are controlled by a traffic light, internal junctions are built for every stream that has a *green minor* phase (dark green). Thus, loading custom traffic light plans during network building may influence the building of internal junctions.

Since version 0.25.0 the user also has the option for [customizing the presence and location of internal junctions](/Networks/Building_Networks_from_own_XML-descriptions#Explicitly_setting_which_Edge_.2F_Lane_is_connected_to_which "wikilink").

Junction Blocking
=================

In most jurisdictions, drivers are forbidden to enter an intersection if the outbound road is jammed to prevent them from blocking the intersection. By default, vehicles in SUMO try to prevent blocking intersections. This is accomplished by the **no-block-heuristic** which prevents them from driving onto the intersection if they are likely to become stuck there. This heuristic may be disabled by modifying the simulation network ahead of the simulation. .

[NETCONVERT](/NETCONVERT "wikilink") options for allowing drivers to drive onto an intersections
------------------------------------------------------------------------------------------------

-   setting option (default *true*) will cause the **no-block-heuristic** to be disabled for all intersections.
-   setting [-attribute](/Networks/Building_Networks_from_own_XML-descriptions#Node_Descriptions "wikilink")
-   setting [-attribute](/Networks/Building_Networks_from_own_XML-descriptions#Connection_Descriptions "wikilink") will cause the **no-block-heuristic** to be disabled for vehicles entering the intersection via that connection

Junction model attributes for allowing drivers to drive onto an intersection
----------------------------------------------------------------------------

By setting the junction model parameter *jmIgnoreKeepClearTime* in a -definition, drivers of that type will ignore the **no-block-heuristic** after their accumulated waiting time exceeds the parameter value (in seconds).

Ignoring blocking vehicles after some time
------------------------------------------

When vehicles in SUMO are unable to move for some time they will be [teleported](/Simulation/Why_Vehicles_are_teleporting#Waiting_too_long.2C_aka_Grid-locks "wikilink") to resolve dead-lock. If this is not desired, [SUMO](/SUMO "wikilink")-option may be used to ignore vehicles which are blocking the intersection on an intersecting lane after the specified time. This can be used to model the real-life behaviour of eventually finding a way around the offending vehicle that is blocking the intersection.

Customizing Behavior at Junctions
=================================

TraCI
-----

The speed of a vehicle may be set using the [speed command](/TraCI/Change_Vehicle_State#Command_0xc4:_Change_Vehicle_State "wikilink"). When combined with [speed mode command](/TraCI/Change_Vehicle_State#speed_mode_.280xb3.29 "wikilink") various safety-related rules can be disabled. Among them are flags for

-   overriding save speed in regard to leader vehicles, or vehicles already on the intersection
-   ignoring right-of-way rules
-   ignore red lights

Driver Parameters
-----------------

The behavior at intersections can be configured with [junction model parameters](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Junction_Model_Parameters "wikilink"). The following aspects can be affected

-   aggressiveness when merging from a unprioritized road (*impatience*)
-   distance-keeping to pedestrians
-   driving onto an intersection inspite of [\#Junction_Blocking](/#Junction_Blocking "wikilink") rules
-   ignoring red lights
    -   speed when ignoring red lights
