---
layout: post
title: IntermodalRouting
permalink: /IntermodalRouting/
---

__FORCETOC__

Basic Concepts
==============

Every person may have multiple modes of transport to chose from. Currently those are walking (which is assumed to be always possible), riding by public transport and going by car. Intermodal routing uses person trips to define a trip of a person including mode changes. Currently only the [DUAROUTER](/DUAROUTER "wikilink") can handle this input.

Defining intermodal demand
==========================

To define intermodal demand use the -element:

    <routes>
         <person id="p0" depart="0">
            <personTrip from="beg" to="end"/>
        </person>
    </routes>

The tool [randomTrips.py](/Tools/Trip#randomTrips.py "wikilink") may be used with the option to generate random intermodal demand.

Defining available cars
=======================

To allow usage of a car, either the attribute or the vType of the available car must be specified for the personTrip:

    <routes>
        <vType id="typ0" vClass="passenger"/>
        <person id="p0" depart="0">
            <personTrip from="beg" to="end" vTypes="typ0"/>
        </person>
    </routes>

Defining public transport
=========================

Every vehicle with a line attribute is considered public transport and will be used for routing regardless of its capacity.

    <routes xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://sumo.dlr.de/xsd/routes_file.xsd">
        <flow id="bus" from = "beg" to ="end" line="bus" begin="0" end="1000" period="300">
                    <stop busStop="beg_0" until="10"/>
                    <stop busStop="left_0" until="110"/>
                    <stop busStop="end_0" until="210"/>
        </flow>
        <person id="p0" depart="0">
            <personTrip from="beg" to="end" modes="public"/>
        </person>
    </routes>

-   In order to define a route-able bus schedule all -definitions must use the *until*-attribute.
-   Stops that are declared as child elements of a flow must have until times appropriate for the first vehicle in the flow. The until times for later vehicles will be shifted forward by the flow period
-   Stops that are declared as child element of a stand-alone route (external to a flow or vehicle) must have until times that are offsets from the departure time of the respective vehicles.

Intermodal Cost Function
========================

Generally, intermodal routing may consider multiple criteria such as travel time, costs, reliability and convenience. Currently, [DUAROUTER](/DUAROUTER "wikilink") only takes the following travel time into account:

-   Individual vehicle transport uses the standard vehicle routing costs. This can be influenced by loading custom weights via option
-   Walking uses the maximum walking speed of the person and multiplies this with a factor, configurable via option (default *0.9*). The factor is used to account for delays due to intersections and pedestrian interactions
-   Public transport uses the difference of the *until*-times between successive stops
-   [Accessing a stop from another part of the network](/Simulation/Public_Transport#Access_Lanes "wikilink") currently takes no additional time (this will be configurable in the future)
