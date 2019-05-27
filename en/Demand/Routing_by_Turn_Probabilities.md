---
layout: post
title: Demand Routing by Turn Probabilities
permalink: /Demand/Routing_by_Turn_Probabilities/
---

The [JTRROUTER](/JTRROUTER "wikilink") is a routing applications which uses flows and turning percentages at junctions as input. The following parameter must be supplied:

-   the network to route the vehicles through,
-   the description of the turning ratios for the junctions (defaults may be used for this, too), and
-   the descriptions of the flows.

A call may look like this:

`jtrrouter --flow-files=`<FLOW_DEFS>` --turn-ratio-files=`<TURN_DEFINITIONS>` --net-file=`<SUMO_NET>` \`
`  --output-file=MySUMORoutes.rou.xml --begin `<UINT>` --end `<UINT>

Turn Definitions
----------------

To describe the turn definitions, one has to write an XML file. Within this file, for each interval and each edge the list of percentages to use a certain follower edge has to be given. An example:

    <turns>
       <interval begin="0" end="3600">
          <fromEdge id="myEdge0">
             <toEdge id="myEdge1" probability="0.2"/>
             <toEdge id="myEdge2" probability="0.7"/>
             <toEdge id="myEdge3" probability="0.1"/>
          </fromEdge>

          ... any other edges ...

       </interval>

       ... some further intervals ...

    </turns>

The snippet defines that vehicles coming at the end of edge “<span class="inlxml">myEdge0</span>” within the time interval between 0s and 3600s will choose the edge “<span class="inlxml">myEdge1</span>” with a probability of 20%, “<span class="inlxml">myEdge2</span>” with a probability of 70% and “<span class="inlxml">myEdge3</span>” with a probability of 10%. Another possibility to save time on preparing the description is to use default values. The parameter can be used to describe the default ratios that will be used for all junctions for all time steps. <TURN_DEFAULTS> is a list of doubles, separated by a ','. To achieve the same behaviour as in the example above, use . The values will be applied to an edge's following edges beginning at the right edge (20%) and ending at the leftmost edge (10%). As the number of possible followers changes for different edges, the values are resampled for edges which number of following edges differs from the number of given turning probability defaults. Given a vehicle using an edge that has two followers would use the follower to the right with 55% probability, the one to the left with 45%.

### Automatic generation of turn definitions

For automatic, yet artificial, turn definitions generation based on the network structure, see [generateTurnDefs.py](/Tools/Misc#generateTurnDefs.py "wikilink").

Sinks Definitions
-----------------

A vehicle leaves the network as soon as it comes to a sink edge. As not all networks have sink edges defined, one can support a list of edges to be declared as sinks using . You may also add your sink definitions to a turn-file (XML only):

    <turns>
       ... some further turning definitions as above ...

       <sink edges="<EDGE_ID>[ <EDGE_ID>]*"/>
       ... further sink definitions ...

    </turns>

If you do not define sinks, the option may be used to declare all edge as possible sinks.

Flow Definitions
----------------

The [definitions of the flow](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Repeated_vehicles_.28Flows.29 "wikilink") is the same as for the [DUAROUTER](/DUAROUTER "wikilink") with just a single difference: as it is not known where the vehicle will leave the network as the route it uses is randomly computed, the route must be specified using attribute *from* and attribute *to* must be omitted:

` `<flow id="0" from="A" begin="0" end="3600" probability="0.5"/>

Additional Options
------------------

As theoretically a route may get infinitely long when a vehicle is forced to take always the same direction, it is possible to limit the route's size using optoin . This factor, multiplied with the number of the used network's edges is the maximum number of edges a route may have. With the default of 2.0, a route may contain twice as many edges as the network has. Any route longer than this size will be marked as invalid. We assume that for each network this number has to be chosen again.