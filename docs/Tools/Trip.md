---
layout: post
title: Tools Trip
permalink: /Tools/Trip/
---

__FORCETOC__

randomTrips.py
==============

“randomTrips.py” generates a set of random trips for a given network (option ). It does so by choosing source and destination edge either uniformly at random or with a modified distribution as described below. The resulting trips are stored in an XML file (option , default trips.trips.xml) suitable for [DUAROUTER](/DUAROUTER "wikilink") which is called automatically if the option (with a filename for the resulting route file) is given. The trips are distributed evenly in an interval defined by begin (option , default 0) and end time (option , default 3600) in seconds. The number of trips is defined by the repetition rate (option , default 1) in seconds. Every trip has an id consisting of a prefix (option , default "") and a running number. Example call:

`/tools/randomTrips.py -n input_net.net.xml -e 50 `

The script does not check whether the chosen destination may be reached from the source. This task is performed by the router. If the network is not fully connected some of the trips may be discarded.

The option ensures a minimum straight-line distance (in meter) between start and end edges of a trip. The script will keep sampling from the edge distribution until enough trips with sufficient distance are found.

Randomization
-------------

When running *randomTrips.py* twice with the same parameters, different output files will be created due to randomness. The option can be used to get repeatable pseudo-randomness.

Edge Probabilities
------------------

The option increases the probability that trips will start/end at the fringe of the network. If the value *10* is given, edges that have no successor or no predecessor will be 10 times more likely to be chosen as start- or endpoint of a trip. This is useful when modelling through-traffic which starts and ends at the outside of the simulated area.

The probabilities for selecting an edge may also be weighted by

-   edge length (option ),
-   by number of lanes (option )
-   edge speed (exponentially, by option )

For additional ways to influence edge probabilities call

`/tools/randomTrips.py --help`

Arrival rate
------------

The arrival rate is controlled by option (*default 1*). By default this generates vehicles with a constant period and arrival rate of (1/period) per second. By using values below 1, multiple arrivals per second can be achieved.

When adding option the arrivals will be randomized using a binomial distribution where *n* (the maximum number of simultaneous arrivals) is given by the argument to and the expected arrival rate is 1/period *(this option is not yet available in version 0.23.0)*.

### Example

To let *n* vehicles depart between times *t0* and *t1* set the options

`-b `*`t0`*` -e `*`t1`*` -p `*`((t1`` ``-`` ``t0)`` ``/`` ``n)`*

Validated routes and trips
--------------------------

When using the option , an output file with valid vehicle routes will be generated. This works by automatically calling [DUAROUTER](/DUAROUTER "wikilink") in the background to turn the random trips into routes and automatically discard disconnected trips. It may be necessary to increase the number of generated random trips to account for a fraction disconnected, discarded trips.

Sometimes it is desirable to obtain validated trips rather than routes (i.e. to make use of [one-shot route assignment](/Demand/Dynamic_User_Assignment#oneShot-assignment "wikilink"). In this case the additional option may be used to generate validated trips (by first generating valid routes and then converting them back into trips).

Generating vehicles with additional parameters
----------------------------------------------

With the option , additional parameters can be given to the generated vehicles (note, usage of the quoting characters).

` ``/tools/randomTrips.py -n input_net.net.xml --trip-attributes=`“`departLane=\`”`best\" departSpeed=\`“`max\`”` departPos=\`“`random\`”`"`

This would make the random vehicles be distributed randomly on their starting edges and inserted with high speed on a reasonable lane.

### Setting a vehicle type from an external file

If the generated vehicles should have a specific vehicle type, an needs to be prepared:

<additional>
`  `<vType id="myType" maxSpeed="27" vClass="passenger"/>
</additional>

Then load this file (assume it was saved as *type.add.xml*) with the option --additional-file

`/tools/randomTrips.py -n input_net.net.xml --trip-attributes=`“`type=\`”`myType\"" --additional-file type.add.xml `
`   --edge-permission passenger`

Note the use of the option (deprecated alias: ) which ensures that random start- and arrival-edges allow a specific vehicle class.

To generate random pedestrian traffic instead of vehicular traffic, the option may be used. It is recommended to combined this with the option to avoid walks of excessive length. See [Simulation/Pedestrians](/Simulation/Pedestrians "wikilink") for addition information on the simulation of pedestrians.

Note that the option should only be used as a quick shorthand to generate trips for the standard type of the given vehicle class since it places a standard vType definition in the generated trips file.

### Automatically generating a vehicle type

By setting the option a vehicle type definition that specifies vehicle class will be added to the output files. I.e.

` randomTrips.py --vehicle-class bus ...`

will add

` `<vType id="bus" vClass="bus"/>

After *randomTrips.py* has finished, the created -element can be edited to specify additional parameters. In contrast to the above method with an , manual editing must be repeated when running *randomTrips.py* again.

Generating different modes of traffic
-------------------------------------

-   Using the option will generated pedestrians instead of vehicles.
-   Using the option will generated persons with definitions. This means they will use [IntermodalRouting](/IntermodalRouting "wikilink") to decided whether they use public transport or walking.

Intermediate Way Points
-----------------------

To generate longer trips within a network, intermediate way points may be generated using the option . This will add the given number of [via-edges](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Incomplete_Routes_.28trips_and_flows.29 "wikilink") to the trip definitions.

Customized Weights
------------------

### Saving

Using option will cause three *weight-files* with the given prefix to be generated (*<prefix>.src.xml, <prefix>.dst.xml, <prefix>.via.xml*) which contain the used edge probabilities.

-   *.src.xml* contains the probabilities for an edge to be selected as -edge
-   *.dst.xml* contains the probabilities for an edge to be selected as -edge
-   *.via.xml* contains the probabilities for an edge to be selected as -edge (only used when option is set).

### Visualization

Any of these files can be loaded in [SUMO-GUI](/SUMO-GUI "wikilink") for visualization, i.e. using the options . In [SUMO-GUI](/SUMO-GUI "wikilink") lane-coloring *by loaded weight* must be selected to make the data visible.

Note, that the elements within the weight files are only used when visualizing the files in this way.

### Loading

Files in this format can be used to set customized weights for generating random trips by using the option with the prefix value as argument. The randomTrips script will attempt to load weights for all edges and all three file extensions (*.src.xml, .dst.xml, .via.xml*) but will use the following defaults if same values are missing:

-   If a loaded weight file does not contain all edges, probability 0 will be assumed for the missing edges
-   If a file is missing, the probabilities according to the regular options are used when sampling that type of edge (i.e. missing *<prefix>.dst.xml* will result in probabilities as described in section [\#Edge_Probabilities](/#Edge_Probabilities "wikilink") will be used when sampling destination edges)

### Usage Example

To obtain trips from two specific locations (edges *a*, and *b*) to random destinations, use

` randomTrips.py --weights-prefix example  ...`<other options>`...`

and define only the file *example.src.xml* as follows:

` `<edgedata>
`   `<interval begin="0" end="10"/>
`     `<edge id="a" value="0.5"/>
`     `<edge id="b" value="0.5"/>
`   `</interval>
` `</edgedata>

route2trips.py
==============

This script generates a trip file from a route file by stripping all route information except for start and end edge. It has a single parameter which is the route file and prints the trip file to stdout. Example:

`/tools/route2trips.py input_routes.rou.xml`