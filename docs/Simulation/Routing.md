---
title: Simulation Routing
permalink: /Simulation/Routing/
---

Features that cause rerouting
=============================

There are multiple simulation features that allow routing at simulation time. They are described in the following:

Routing triggered by the vehicle
--------------------------------

This type of routing works by assigning a *rerouting device* to some or all vehicles. Details are given at [Demand/Automatic_Routing](/Demand/Automatic_Routing "wikilink").

Incomplete Trips and Flows
--------------------------

This is a special case of the above method. Vehicles with incomplete routes automatically receive a *rerouting device* and are rerouted once when entering the network. In some scenarios this is a practical [*one-shot*-approach to route assignment](/Demand/Dynamic_User_Assignment#oneShot-assignment "wikilink") that avoids time-consuming [iterative assignment](/Demand/Dynamic_User_Assignment#General_behavior "wikilink").

Alternative Route Signage
-------------------------

This is a location based method for triggering rerouting and is described at [Simulation/Rerouter](/Simulation/Rerouter "wikilink").

TraCI
-----

Using the methods [*change target* or *reroute*](/TraCI/Change_Vehicle_State "wikilink") rerouting is triggered for the specified vehicle.

Alternative Destinations
========================

By using [-definitions](/Simulation/Rerouter "wikilink"), vehicles can be routed to alternative destinations. A different method is to use [traffic assignment zones (TAZ)](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Traffic_assignement_zones_.28TAZ.29 "wikilink"). This allows vehicles to change their destination to the best alternative from a list of potential destinations.

Travel-time values for routing
==============================

By default, the route with the least travel time is chosen. The following order of steps is taken to retrieve the travel time for each edge (If one step fails due to lack of data, the next step is taken):

1.  The vehicle retrieves it's individual data storage. This can be set and retrieved using the TraCI vehicle methods [*change edge travel time information*](/TraCI/Change_Vehicle_State#change_edge_travel_time_information_.280x58.29 "wikilink") and [*edge travel time information*](/TraCI/Vehicle_Value_Retrieval#edge_travel_time_information_.280x58.29 "wikilink").
2.  The [global edge weights](/Demand/Shortest_or_Optimal_Path_Routing#Custom_edge_weights "wikilink") loaded using option are retrieved.
3.  The global edge weights (set and retrieved via TraCI) using the TraCI edge methods [*change edge travel time information*](/TraCI/Change_Edge_State "wikilink") and [*edge travel time information*](/TraCI/Edge_Value_Retrieval "wikilink").
4.  The minimum travel time (length/allowedSpeed) is used.

Special cases
-------------

-   When rerouting with the *rerouting device* the travel time always comes from another data storage which is updated continuously with a configurable averaging procedure. The [parameters for this updating strategy are user definable](/Demand/Automatic_Routing "wikilink"). It is also possible to [set the device travel time directly via TraCI](/TraCI/Change_Vehicle_State#Supported_Device_Parameters "wikilink").
-   When using the TraCI method rerouteTraveltime from the [python TraCI library](/TraCI/Interfacing_TraCI_from_Python "wikilink"), the command supports an additional boolean parameter *currentTravelTime* (default *True*). When this parameter is set to *True*, the global edge weights are replaced by to the currently measured travel times before rerouting. To replicate this behavior with other TraCI clients, all edges in the network must be called with *change global travel time information* using the value of *current travel time*. Note that the travel time values which are set in this way are used for the full duration of the simulation unless updated again.

Routing by *effort*
===================

When setting the option , additional routing efforts are read according to the specified attribute. These are only used when calling the TraCI function [reroute by effort](/TraCI/Change_Vehicle_State "wikilink"). The assumed efforts along a vehicles route are are time-based values and the time is computed based on the travel time values described above.

Routing Algorithms
==================

Applications that perform routing ([SUMO](/SUMO "wikilink"), [SUMO-GUI](/SUMO-GUI "wikilink"), [DUAROUTER](/DUAROUTER "wikilink"), [MAROUTER](/MAROUTER "wikilink")) support the option for selecting among the following values:

-   *dijkstra*: (default) [Dijkstras](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm) algorithm is the simplest and slowest of routing algorithms. It is well suited to routing in time-dependent networks (i.e. when the travel time on an edge depends on the time of day)
-   *astar*: The [A\*](https://en.wikipedia.org/wiki/A*_search_algorithm) routing algorithm uses a metric for bounding travel time to direct the search and is often faster than dijkstra. Here, the metric ''euclidean distance / maximumVehicleSpeed) is used.
    -   by using *astar* together with the option the ALT-Algorithm is activated (A\*, Landmarks, triangle inequality). It uses a precomputed distance table to selected network edges (so-called landmarks) to speed up the search, often by a significant factor.
    -   by using *astar* together with the option the A\* algorithm is used together with a complete (and often huge) distance table to allow for blazing fast search.
-   *CH*: [Contraction Hierarchies](https://en.wikipedia.org/wiki/Contraction_hierarchies) is preprocessing-based routing algorithm. This is very efficient when a large number of queries is expected. The algorithm does consider time-dependent weights. Instead, new preprocessing can be performed for time-slices of fixed size by setting the option . The preprocessing is done without restrictions on vehicle class which reduces efficiency in multi-modal networks.
-   *CHWrapper*: This works like *CH* but performs separate preprocessing for every vehicle class that is encountered, thereby increasing routing efficiency.
