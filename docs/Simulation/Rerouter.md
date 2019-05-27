---
layout: post
title: Simulation Rerouter
permalink: /Simulation/Rerouter/
---

Rerouter
========

Rerouter changes the route of a vehicle as soon as the vehicle moves onto a specified edge.

A rerouter is set into the simulated network by adding the following declaration line to an : <span class="inlxml"><rerouter id="<REROUTER_ID>" edges=“<EDGE_ID>\[;<EDGE_ID>\]\*” file=“<DEFINITION_FILE>” \[probability=“<PROBABILITY>”\]/&gt;</span>. Rerouter may be placed on several edges, at least one edge is necessary. Furthermore, it is possible to define the probability for rerouting a vehicle by giving a number between 0 (none) and 1 (all) already within the definition. The declaration values are:

| Attribute Name | Value Type  | Description                                                                                            |
|----------------|-------------|--------------------------------------------------------------------------------------------------------|
| **id**         | id (string) | The id of of the rerouter                                                                              |
| **edges**      | float       | An edge id or a list of edge ids where vehicles shall be rerouted                                      |
| file           | float       | The path to the definition file (alternatively, the intervals may defined as children of the rerouter) |
| probability    | float       | The probability for vehicle rerouting (0-1), default 1                                                 |
| off            | bool        | Whether the router should be inactive initially (and switched on in the gui), *default:false*          |

A rerouter may work in several different ways. Within a time period you may close an edge, or assign new destinations or predefined routes to vehicles. The next sections will describe these actions in detail.

Definition styles
-----------------

There are two styles in which to declare rerouters.

### everything in one file

The looks like this:

    <additional>
       <rerouter id="<REROUTER_ID>" edges="<EDGE_ID>[;<EDGE_ID>]*" [probability="<PROBABILITY>"]>
           <interval begin="<BEGIN_TIME>" end="<END_TIME>">
              ... action description ...
           </interval>

           ... further intervals ...
       </rerouter>

       ... further rerouters ...
    </additional>

### definitions in a separate file

The looks like this:

    <additional>
       <rerouter id="<REROUTER_ID>" edges="<EDGE_ID>[;<EDGE_ID>]*" file="<DEFINITION_FILE>" [probability="<PROBABILITY>"]/>

       ... further rerouters ...
    </additional>

And the <DEFINITION_FILE> (which describes the actions over time) looks like this:

    <rerouter>
       <interval begin="<BEGIN_TIME>" end="<END_TIME>">
          ... action description ...
       </interval>

       ... further intervals ...

    </rerouter>

Note, that the name of the root-level element ( in this case) is arbitrary.

Closing a Street
----------------

A “closingReroute” forces the rerouter to close the edge <EDGE_ID>. Vehicles which normally would pass this edge will get a new route as soon as they reach one of the edges given in the edges-attribute of the rerouter's declaration. The algorithm for selecting a new route is the same as described at [\#Assigning_a_new_Destination](/#Assigning_a_new_Destination "wikilink") with the additional constraint that closed edges must be avoided. A closingReroute definition may look like this:

    <rerouter>
       <interval begin="<BEGIN_TIME>" end="<END_TIME>">
          <closingReroute id="<EDGE_ID>"/>
       </interval>

       ... further intervals ...

    </rerouter>

The attributes used within such definitions are:

| Attribute Name | Value Type              | Description                                                                                                                                                                                                                 |
|----------------|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **id**         | id (string)             | The id of the closed edge; the id must be the id of an edge within the network                                                                                                                                              |
| allow          | list of vehicle classes | The (optional) ' '-separated list of [vehicle classes](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Abstract_Vehicle_Class "wikilink") which are still allowed to drive on the closed edge. All others are forbidden. |
| disallow       | list of vehicle classes | The (optional) ' '-separated list of [vehicle classes](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Abstract_Vehicle_Class "wikilink") which are forbidden from driving on the closed edge. All others are allowed.   |

When using a without attributes and , vehicles that cannot reach their destination by an alternative route simply continue on their old route and will effectively ignore the closing of the edges. When using either attribute or (only one may be used in the same definition), vehicles which cannot change their route will stop in front of the closed edge until the defined interval ends. This may be used to simulate traffic jams, caused by spontaneous road closing.

Closing a Lane
--------------

A “closingLaneReroute” forces the rerouter to close the lane <LANE_ID> by setting its permissions to *authority* (this can be customized). Vehicles that pass this route and which are equipped with a [rerouting device](/Demand/Automatic_Routing "wikilink") may compute a new route as soon as they reach one of the edges given in the edges-attribute of the rerouter's declaration. A closingLaneReroute definition may look like this:

    <rerouter>
       <interval begin="<BEGIN_TIME>" end="<END_TIME>">
          <closingLaneReroute id="<LANE_ID>"/>
       </interval>

       ... further intervals ...

    </rerouter>

The attributes used within such definitions are:

| Attribute Name | Value Type              | Description                                                                                                                                                                                                                                                                                                                        |
|----------------|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **id**         | id (string)             | The id of the closed lane; the id must be the id of a lane within the network                                                                                                                                                                                                                                                      |
| allow          | list of vehicle classes | The (optional) ' '-separated list of [vehicle classes](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Abstract_Vehicle_Class "wikilink") which are still allowed to drive on the closed edge. All others are forbidden. (default *authority*)                                                                                  |
| disallow       | list of vehicle classes | The (optional) ' '-separated list of [vehicle classes](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Abstract_Vehicle_Class "wikilink") which are forbidden from driving on the closed edge. All others are allowed. (This attribute may be used instead of **allow** for brevity if only a few classes shall be disallowed). |

Assigning a new Destination
---------------------------

A “dest_prob_reroute” forces the rerouter to assign a new route to vehicles that pass one of the edges defined in the edges-attribute of the rerouter's declaration. A new route destination is used, defined by the name of a new destination in the according element:

    <rerouter>
       <interval begin="<BEGIN_TIME>" end="<END_TIME>">
          <destProbReroute id="<EDGE_ID1>" probability="<PROBABILITY1>"/>
          <destProbReroute id="<EDGE_ID2>" probability="<PROBABILITY2>"/>
       </interval>

       ... further intervals ...

    </rerouter>

The fastest route is computed automatically using the Dijkstra-algorithm and starting at the edge the vehicle is located at and ending at the new destination. The following travel times are considered for routing (the first applicable value is used):

-   the current (smoothed) travel times in the network are used if the vehicle is equipped with a [rerouting device](/Demand/Automatic_Routing "wikilink")
-   subjective edge costs for the current vehicle if set via[TraCI command *change edge travel time information*](/TraCI/Change_Vehicle_State#change_edge_travel_time_information_.280x58.29 "wikilink")
-   edge weights loaded via the [SUMO](/SUMO "wikilink") option
-   travel times in the empty network

The attributes used within a dest_prob_reroute are:

| Attribute Name  | Value Type                        | Description                                                                                                                                         |
|-----------------|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| **id**          | id (string)                       | The id of the new destination; the id must be the id of an edge within the network or one of the special values *keepDestination*, *terminateRoute* |
| **probability** | float (should be between 0 and 1) | The probability with which a vehicle will use the given edge as destination; the probabilities are automatically normalized to sum to 1             |

### Special Destination Values

-   *keepDestination*: the vehicle continues on its current route
-   *terminateRoute*: the vehicle immediately leaves the simulation and counts as arrived at its current position on the rerouter edge

Assigning a new Route
---------------------

A “route_prob_reroute” forces the rerouter to assign a new route to vehicles which pass one of the edges defined in the edges-attribute of the rerouter's declaration. In this case, the id of a complete route must be supplied instead of a new destination:

    <rerouter>
       <interval begin="<BEGIN_TIME>" end="<END_TIME>">
          <routeProbReroute id="<ROUTE_ID1>" probability="<PROBABILITY1>"/>
          <routeProbReroute id="<ROUTE_ID2>" probability="<PROBABILITY2>"/>
       </interval>

       ... further intervals ...

    </rerouter>

The attributes used within such definitions are:

| Attribute Name | Value Type  | Description                                                                                                                                                  |
|----------------|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **id**         | id (string) | The id of a new route to assign; the id must be the id of a previously loaded route                                                                          |
| probability    | float       | The the probability with which a vehicle will use the given edge as destination; (default 1). The probabilities are automatically normalized for all entries |

Rerouting to an alternative Parking Area
----------------------------------------

Vehicles that stop at a [parking area](/Simulation/ParkingArea "wikilink") may encounter the situation that the parking area has reached the limit of its capacity and does not permit parking.

In this case the vehicle either waits on the road until a parking space becomes available or it may reroute to an alternative parking area. For the latter behaviour a -definition must be specified. This rerouter definition defines a set of parking areas that may be mutually used as alternatives. Rerouting two another parking area is triggered in two cases:

-   when a vehicle reaches a parkingArea and is unable to stop due to lack of capacity
-   when a vehicle enters one of the rerouter-edges and the next parkingArea on it's route is filled to capacity

The definition looks like this:

       <rerouter id="myRerouter" edges="a b">
          <interval begin="0" end="2000">
             <parkingAreaReroute id="ParkAreaA"/>
             <parkingAreaReroute id="ParkAreaB"/>
          </interval>
       </rerouter>

The attributes used within such definitions are:

| Attribute Name | Value Type  | Description                                                                                                                                                 |
|----------------|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **id**         | id (string) | The id of an existing parking area                                                                                                                          |
| probability    | float       | The probability for each of the alternatives to be selected (default 1). The probabilities are automatically normalized over all definitions in a rerouter. |

### Determining the alternative parking area

The alternative parkingArea will be selected among all parking areas that have at least 1 free space according to the minimum weighted sum over a number of attributes. By default only the distance from the current vehicle position to the new parking area is considered. The following table describes the weighting factors that can be customized using [generic parameters of the vehicle or its vType](/Simulation/GenericParameters "wikilink"):

| Parameter Name              | Default value | Description                                                              | Inverse (Bigger is better) |
|-----------------------------|---------------|--------------------------------------------------------------------------|----------------------------|
| parking.probability.weight  | 0             | the influence of the *probability* attribute of the                      | yes                        |
| parking.capacity.weight     | 0             | The total capacity of the parking area                                   | yes                        |
| parking.capacity.weight     | 0             | The total capacity of the parking area                                   | yes                        |
| parking.absfreespace.weight | 0             | The absolute number of free spaces                                       | yes                        |
| parking.relfreespace.weight | 0             | The relative number of free spaces                                       | yes                        |
| parking.distanceto.weight   | 1             | The road distance to the parking area                                    | no                         |
| parking.timeto.weight       | 0             | The assumed travel time to the parking area                              | no                         |
| parking.distancefrom.weight | 0             | The road distance from the parking area to the vehicles destination      | no                         |
| parking.timefrom.weight     | 0             | The assumed travel time from the parking area to the vehicle destination | no                         |
||

### Destination after rerouting

Generally, vehicles that reroute to a new parking area will continue to their original destination after finishing the stop. In the special case where

1.  the original route ended at the original parkingArea edge and
2.  the arrivalPos was within \[startPos, endPos\] of the original parkingArea

then the new route will also end at the new parkingArea and the endPos of the new parkingArea will be set as new arrivalPos.