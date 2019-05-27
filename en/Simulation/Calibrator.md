---
layout: post
title: Simulation Calibrator
permalink: /Simulation/Calibrator/
---

__TOC__

Calibrators
===========

These trigger-type objects may be specified within an and allow the dynamic adaption of traffic flows and speeds. The syntax for such an object is: <span class="inlxml"><calibrator id="<ID>" lane=“<LANE_ID>” output=“<OUTPUT_FILE>”/&gt;</span>. They can be used to modify simulation scenario based on induction loop measurements. A calibrator will remove vehicles in excess of the specified flow and it will insert new vehicles if the normal traffic demand of the simulation does not meet the specified number of . Furthermore, the speed on the edge will be adjusted to the specified similar to the workings of a [variable speed sign](/Simulation/Variable_Speed_Signs "wikilink"). Calibrators will also remove vehicles if the traffic on their lane is jammend beyond what would be expected given the specified flow and speed. This ensures that invalid jams do not grow upstream past a calibrator.

    <additional>
      <vType id="t0" speedDev="0.1" speedFactor="1.2" sigma="0"/>
      <route id="c1" edges="beg middle end rend"/>

      <calibrator id="calibtest_edge" edge="beg" pos="0" output="detector.xml">
        <flow begin="0"    end="1800" route="c1" vehsPerHour="2500" speed="27.8" type="t0" departPos="free" departSpeed="max"/>
        <flow begin="1800" end="3600" route="c1" vehsPerHour="2500" speed="15.0" type="t0" departPos="free" departSpeed="max"/>
      </calibrator>

      <calibrator id="calibtest_lane" edge="middle_1" pos="0" output="detector.xml">
        <flow begin="0"    end="1800" route="c1" vehsPerHour="600" speed="27.8" type="t0" departPos="free" departSpeed="max"/>
        <flow begin="1800" end="3600" route="c1" vehsPerHour="800" speed="15.0" type="t0" departPos="free" departSpeed="max"/>
      </calibrator>

    </additional>

The following attributes/elements are used within the calibrator element:

| Attribute Name | Value Type    | Description                                                                                                                                         |
|----------------|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| **id**         | id (string)   | The id of the calibrator                                                                                                                            |
| edge           | id (string)   | The id of an edge for measuring and calibrating flow. (Either *edge* or *lane* must be specified)                                                   |
| lane           | id (string)   | The id of a lane for measuring and calibrating flow (Either *edge* or *lane* must be specified)                                                     |
| **pos**        | float         | The position of the calibrator on the specified lane (currently ignored, see [1](http://sumo-sim.org/trac.wsgi/ticket/1331)                         |
| freq           | float         | The aggregation interval in which to calibrate the flows. default is step-length                                                                    |
| routeProbe     | float         | The id of the [routeProbe](/Simulation/Output/RouteProbe "wikilink") element from which to determine the route distribution for generated vehicles. |
| output         | file (string) | The output file for writing calibrator information or *NULL*                                                                                        |
||

The elements which are defined as children of the calibrator definition follow the general [format of flow definitions](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Repeated_vehicles "wikilink"). As the only difference, either the attribute or (or both) must be given.

By default edge calibrators will use whereas lane calibrators will use where *x* is the lane index of the calibrator lane. All calibrators default to .

Routes of generated Vehicles
----------------------------

Whenever the measured flow in a given interval is lower than the specified flow, new vehicles are inserted. If the attribute is specified, a route is sampled from the distribution of the named [route probe detector](/Simulation/Output/RouteProbe "wikilink"). Otherwise the attribute of the flow is used. Note, that this value may also specify the name of a route distribution.

The algorithm for deciding when exactly to insert (and remove) vehicles is described in [Erdmann, Jakob (2012) Online-Kalibrierung einer Mikroskopischen Verkehrssimulation. ViMOS 2012, 29.11.2012, Dresden, Deutschland.](http://elib.dlr.de/79428/)

Building a scenario without knowledge of routes, based on flow measurements
---------------------------------------------------------------------------

Due to their ability of adapting higher as as well as lower flows to a specified value, calibrators may be used to adapt (almost) arbitrary traffic demand to a given set of measurements. One strategy for building a scenario from measurements is therefore, to [generated random traffic](/Tools/Trip#randomTrips.py "wikilink") and use Calibrators in conjunction with [route probe detectors](/Simulation/Output/RouteProbe "wikilink"). While this can in principle be done with [DFROUTER](/DFROUTER "wikilink") as well, the method described here is more robust for highly meshed networks as found in cities.

Each edge where measurements are given should receive a calibrator and a route probe detector. As soon as the first vehicle has passed the route probe detector, the calibrator will be able to use that vehicles route. For the calibrator to be able to function before the first vehicle, it needs a *fall back* route which just needs to consist of a single edge (i.e. the edge on which the calibrator is placed).

Example :

<additional>
`   `<vType id="t0" speedDev="0.1"/>
`   `<routeProbe id="cali_edge1_probe" edge="edge1" freq="60" file="output.xml"/>
`   `<calibrator id="cali_edge1" lane="edge1_0" pos="0" output="detector.xml" freq="60" routeProbe="cali_edge1_probe">
`      `<route id="cali1_fallback" edges="edge1"/>
`      `<flow begin="0"    end="1800" route="cal1_fallback" vehsPerHour="2500" speed="27.8" type="t0" departPos="free" departSpeed="max"/>
`      `<flow begin="1800" end="3600" route="cal1_fallback" vehsPerHour="2500" speed="15.0" type="t0" departPos="free" departSpeed="max"/>
`   `</calibrator>
</additional>

Running the simulation with the random demand as well as these and definitions will achieve a simulation in which traffic matches the specified flows at each calibrator edge. However, the realism of traffic flow behind (or between) calibrators depends on the fit between random routes and real-world routes. The importance of this fit increases with the size and complexity of the network between calibrator edges.