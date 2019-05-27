---
title: Demand Automatic Routing
permalink: /Demand/Automatic_Routing/
---

Introduction
============

Routing dynamically in the running simulation may be adequate in the following situations:

-   there is not enough time / computing power to wait for the dynamic user equilibrium
-   changes to the net occur while the simulation is running
-   vehicles need to adapt their route while running

In this case [SUMO](/SUMO "wikilink") may be used directly for routing with either routes or trip files (or a mix) as input.

This routing approach works by giving some or all vehicles the capability to re-compute their route periodically. This routing takes into account the current and recent state of traffic in the network and thus adapts to jams and other changes in the network.

The options listed below allow configuring which of the vehicles shall be equipped, how often rerouting decisions shall be made and how the estimation of travel times is computed from current and recent knowledge.

Options
=======

The options related to this routing are:

| Option | default | Description                                                                                                                        |
|--------|---------|------------------------------------------------------------------------------------------------------------------------------------|
|        | 0       | The probability for a vehicle to have a routing device                                                                             |
|        |         | Assign a device to named vehicles                                                                                                  |
|        | false   | The devices are set deterministic using a fraction of 1000 (with the defined **probability**)                                      |
|        | 0       | The period with which the vehicle shall be rerouted                                                                                |
|        | 60      | The rerouting period before insertion/depart                                                                                       |
|        | 1       | The interval for updating the edge weights.                                                                                        |
|        | 0.5     | The weight of prior edge weights for exponential averaging from \[0, 1\].                                                          |
|        | 0       | The number of adaptation steps for averaging (enable for values &gt; 0).                                                           |
|        | false   | Use [traffic assignment zones (TAZ/districts)](/Demand/Importing_O/D_Matrices#Describing_the_TAZ "wikilink") as routing end points |
|        | false   | Use option for initializing the edge weights at simulation start                                                                   |
||

Edge weights
============

If the routing is enabled for any vehicles, the average travel times in the net are collected for all edges. If a vehicle needs to be routed (either because it gets inserted or because a repeated route choice was enabled via the “.period” option) it chooses the fastest route to its destination edge (or district) according to the present edge weights (travel speeds and hence travel times). The update of the edge weights does not simply overwrite the old value but is computed as a weighted average as described below. Since updating the weights of all edges in each simulation step means a major slowdown for the simulation this interval may be altered using the “.adaption-interval” option.

Adapting by exponential average
-------------------------------

By setting the option the travel speed of each edge is computed as

` FLOAT * priorValue + (1 - FLOAT) * currentMeanSpeed`

This averaging takes place with the period set by .

Adapting by moving average
--------------------------

By setting the option the travel speed of each edge is computed as the average of the INT latest meanSpeed values. This averaging takes place with the period set by .

Incomplete trips and flows
==========================

All vehicles which are created using a trip as input (or a flow with “from” and “to” attributes) get automatically routed at insertion without the need to instantiate the device for them explicitly. Whenever an error occurs on routing because no route can be found which includes all mandatory edges (“from”, “to”, and all stop edges in the correct order) and is connected (also respecting the vehicle class permissions) this is a fatal error and stops th simulation. This can be switched off by using which will leave the route untouched in the error case. If the vehicle did not have a route yet (because it was defined using a trip) and cannot find one and is used, it will not be inserted.

Alternatively to using attributes “from” and “to” it is also possible to use “fromTaz” and “toTaz”, if a [district file is loaded](/Demand/Importing_O/D_Matrices#Describing_the_TAZ "wikilink").

Alternative Declaration via Parameters
======================================

Another way for defining the set of vehicles that are equipped with a rerouting device is via [generic parameters](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Devices "wikilink").

TraCI
=====

The device can be accessed using the TraCI function *vehicle.getParameter* and *vehicle.setParameter*:

**getParameter**

-   device.rerouting.period (returns individual rerouting period in seconds)
-   device.rerouting.edge:EDGE_ID (returns assumed travel time for rerouting where EDGE_ID is the id of a network edge)
-   has.rerouting.device (returns “true” or “false” depending on whether the device is equipped)

**setParameter**

-   device.rerouting.period (double literal, set rerouting period in seconds)
-   device.rerouting.edge:EDGE_ID (double literal, set assumed travel time for rerouting for all vehicles (where EDGE_ID is the id if a network edge). This value is overwritten at the next update interval (--device.rerouting.adaptation-interval).
-   has.rerouting.device (“true”): can be used to dynamically enable automatic rerouting

Randomness
==========

When setting the option , edge weights for routing are dynamically distorted by a random factor drawn uniformly from \[1,\]. This randomization is performed every time an edge weight is used so the same vehicle could select a different route when rerouted on different time steps. The route generated this way may be longer than the fastest route by the given factor (in the worst case). This randomness is a good way to achieve a reasonable route distribution in grid networks an in other cases where many similar route alternatives are available.