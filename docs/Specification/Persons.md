---
title: Specification Persons
permalink: /Specification/Persons/
---

Persons
=======

A person moves through the net by walking or [using vehicles](/Simulation/Public_Transport "wikilink"). The walking behavior is customizable by selecting a [pedestrian model](/Simulation/Pedestrians#Pedestrian_Models "wikilink"). A person element has child elements defining stages of its plan. The stages are a connected sequence of [ride](/Specification/Persons#Rides "wikilink"), [walk](/Specification/Persons#Walks "wikilink") and [stop](/Specification/Persons#Stops "wikilink") elements as described below. Each person must have at least one stage in its plan.

<person id="foo" depart="0">
`    `<walk edges="a b c"/>
`    `<ride from="c" to="d" lines="busline1"/>
`    `<ride .../>
`    `<walk .../>
`    `<stop .../>
</person>

| Attribute | Type      | Range              | Default          | Remark                                                 |
|-----------|-----------|--------------------|------------------|--------------------------------------------------------|
| id        | string    | valid XML ids      | -                |                                                        |
| depart    | float(s)  | ≥0                 | -                |                                                        |
| departPos | float(s)  | ≥0                 | -                | the distance along the edge that the person is created |
| type      | string    | any declared vType | DEFAULT_PEDTYPE | the type should have vClass pedestrian                 |
| color     | rgb color |                    |                  |                                                        |

When specifying a <span class="inlxml">type</span>, the set of attributes which are in effect during simulation depend on the selected [pedestrian model](/Simulation/Pedestrians#Pedestrian_Models "wikilink"). Attributes such as , , and are always used for visualization.

Visualization
-------------

Persons are rendered in the GUI with the configured detail-level. When assigning a type with attribute *imgFile*, the person may be rendered with an image. By default, the image will not be rotated (suitable for abstract icons). However, when setting the types *guiShape*=“pedestrian” the image will be rotated according to the persons location and stage.

Simulation input
================

The input for a person consists of a sequence of *stages* of the 3 types give below.

Rides
-----

Rides define the start and end point of a movement with a single mode of transport (e.g. a car or a bus). They are child elements of plan definitions.

| Attribute  | Type     | Range                     | Default | Remark                                            |
|------------|----------|---------------------------|---------|---------------------------------------------------|
| from       | string   | valid edge ids            | -       | id of the start edge                              |
| to         | string   | valid edge ids            | -       | id of the destination edge                        |
| busStop    | string   | valid bus stop ids        | -       | id of the destination stop                        |
| lines      | list     | valid line or vehicle ids | -       | list of vehicle alternatives to take for the ride |
| arrivalPos | float(m) |                           | -1      | arrival position on the destination edge          |

The vehicle to use has to exist already (either public transport or some existing passenger car) and the route to take is defined by the vehicle. The person enters the vehicle if it stops on the 'from' edge and any of the following conditions are met

-   the vehicle has a triggered stop and the person is position within the range of of the stop.
-   the vehicle has a timed stop and the person is waiting within 10m of the vehicle position

The position of the person is either it's or the arrival position of the preceding plan element

A given bus stop may serve as a replacement for a destination edge and arrival position. If an arrival position is given nevertheless it has to be inside the range of the stop.

Walks
-----

Walks define a [pedestrian movement](/Simulation/Pedestrians "wikilink"). They are child elements of plan definitions.

| Attribute  | Type       | Range              | Default                          | Remark                                                                                                                                |
|------------|------------|--------------------|----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| route      | string     | valid route id     | -                                | the id of the route to walk                                                                                                           |
| edges      | list       | valid edge ids     | -                                | id of the edges to walk                                                                                                               |
| type       | string     | valid vType ids    | the type of the enclosing person | the type of pedestrian (use if the speed or dimensions change for this particular walk)                                               |
| from       | string     | valid edge ids     | -                                | id of the start edge                                                                                                                  |
| to         | string     | valid edge ids     | -                                | id of the destination edge                                                                                                            |
| busStop    | string     | valid bus stop ids | -                                | id of the destination stop                                                                                                            |
| duration   | float(s)   | &gt;0              | -                                | (deprecated, determined by the person type and the pedestrian dynamics)                                                               |
| speed      | float(m/s) | &gt;0              | -                                | (deprecated, determined by the person type and the pedestrian dynamics)                                                               |
| departPos  | float(m)   |                    | 0                                | initial position on the starting edge (deprecated, determined by the departPos of the person or the arrival pos of the previous step) |
| arrivalPos | float(m)   |                    | -1                               | arrival position on the destination edge                                                                                              |

You can define either a -id, or a list of to travel or a and a edge. In the first and second case the route edges are traveled in the listed order. They do not need to be joined in the net. In the latter case a shortest path calculation is performed and it is an error if there is no path connecting and .

When given as router input input using the attributes and will be transformed into a walk using the attribute by routing along edges permissible for pedestrian (i.e. sidewalks).

A given bus stop may serve as a replacement for a destination edge and arrival position. If an arrival position is given nevertheless, it has to be inside the range of the stop.

Stops
-----

Stops define a delay until the next element of a plan is started. They can be used to model activities such as working or shopping. Stops for persons follow the specification at [Specification\#Stops](/Specification#Stops "wikilink"). However, only the attributes , and are evaluated. Using these attributes it is possible to model activities with a fixed duration as well as those with a fixed end time. If a person needs to be transferred between two positions without delay, it is possible to use two stops in conjunction.

Simulation behavior
===================

A person is starting her life at her depart time on the source (resp. first) edge of the first walk, ride or stop. She tries to start the next step of her plan.

Riding
------

The person checks whether a vehicle with a line from the given list is stopping at the given edge. If such a vehicle exists and the person is positioned between the start and end position of the vehicle's stop, the person will enter the vehicle and start its ride. If such a vehicle exists but the person is not positioned between the start and end position of the vehicle's stop, the person will still enter if the vehicle is triggered by the a person and the distance between person and vehicle is at most 10 metres. It does not check whether the vehicle has the aspired destination on the current route. The first time the vehicle stops (on a well defined stop) at the destination edge, the ride is finished and the person proceeds with the next step in the plan.

Walking
-------

The walking behavior of a person depends on the selected [pedestrian model](/Simulation/Pedestrians#Pedestrian_Models "wikilink"). Generally, the person follows the given sequence of edges with a speed bounded by the attribute of the persons type. It starts either at the position from the previous stage of its plan or at the specified if no previous stage exists. The walk concludes at the specified which defaults to the end of the final edge. Both position attributes support the special values and which work as described [for vehicles](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#A_Vehicle.27s_depart_and_arrival_parameter "wikilink").

Stopping
--------

The person stops for the maximum of *currentTime+duration* and *until*.

Router input
============

PersonTrips
-----------

A personTrip defines the start and end point of a movement with optional changes in mode. They are child elements to the person. In order to process a personTrip with mode *public*, the [public transport network](/IntermodalRouting "wikilink") has to be defined as well. Currently bicycle and/or car can only be the first mode. It is not possible to switch to a car or bicycle after a different mode.

| Attribute  | Type     | Range                                         | Default | Remark                                                                                                                                |
|------------|----------|-----------------------------------------------|---------|---------------------------------------------------------------------------------------------------------------------------------------|
| from       | string   | valid edge ids                                | -       | id of the start edge                                                                                                                  |
| to         | string   | valid edge ids                                | -       | id of the destination edge                                                                                                            |
| via        | string   | valid edge ids                                | -       | ids of the intermediate edges (not implemented yet)                                                                                   |
| busStop    | string   | valid bus stop ids                            | -       | id of the destination stop                                                                                                            |
| vTypes     | list     | valid vType ids                               | -       | list of possible vehicle types to take                                                                                                |
| modes      | list     | any combination of “public”, “car”, “bicycle” | -       | list of possible traffic modes. Walking is always possible regardless of this value.                                                  |
| departPos  | float(m) |                                               | 0       | initial position on the starting edge (deprecated, determined by the departPos of the person or the arrival pos of the previous step) |
| arrivalPos | float(m) |                                               | -eps    | arrival position on the destination edge                                                                                              |

Example
=======

The following is an example for a person who walks to a train station, rides the train, alights and walks for a bit, then stops for an activity and finally gets into a car and drives away.

    <routes>
        <person id="person0" depart="0">
            <walk from="2/3to1/3" to="1/3to0/3" departPos="80" arrivalPos="55"/>
            <ride from="1/3to0/3" to="0/4to1/4" lines="train0"/>
            <walk from="0/4to1/4" to="1/4to2/4" arrivalPos="30"/>
            <stop lane="1/4to2/4_0" duration="20" startPos="40" actType="singing"/>
            <ride from="1/4to2/4" to="3/4to4/4" lines="car0"/>
        </person>

        <vehicle id="train0" depart="50">
            <route edges="1/4to1/3 1/3to0/3 0/3to0/4 0/4to1/4 1/4to1/3"/>
            <stop busStop="busStop0" until="120" duration="10"/>
            <stop busStop="busStop1" until="180" duration="10"/>
        </vehicle>

        <vehicle id="car0" depart="triggered">
            <route edges="1/4to2/4 2/4to3/4 3/4to4/4" departPos="30"/>
            <stop lane="1/4to2/4_0" duration="20" startPos="40" endPos="60"/>
        </vehicle>

    </routes>

Person Output
=============

Most of the [Simulation outputs](/Simulation/Output "wikilink") are tailored for vehicles. Only a small number of output formats support persons:

-   [tripinfo-output](/Simulation/Output/TripInfo "wikilink")
-   [vehroute-output](/Simulation/Output/VehRoutes "wikilink")
-   [fcd-output](/Simulation/Output/FCDOutput "wikilink")
-   [netstate-dump](/Simulation/Output/RawDump "wikilink")
-   [aggregated simulation statistics](/Simulation/Output#Aggregated_Traffic_Measures "wikilink")

Planned features
================

The following features are not yet implemented.

-   personFlow is the person equivalent to a vehicle flow. It allows to specify a sequence of persons with the same plan with a single input element.
-   state saving and loading, see
-   TraCI API for persons, see
-   Outputs
    -   include a section for persons in --duration-log.statistics
