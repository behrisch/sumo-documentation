---
layout: post
title: Tools District
permalink: /Tools/District/
---

__TOC__

districts2poly.py
-----------------

Transform [districts](/Demand/Importing_O/D_Matrices#Describing_the_TAZ "wikilink") into polygons for visualization in [SUMO-GUI](/SUMO-GUI "wikilink"). Using the options the colors can be controlled. Each of these options supports values from \[0, 1\] as well as the special value *random*.

`/tools/districts2poly.py myNet.net.xml myDistricts.rou.xml`

edgesInDistricts.py
-------------------

Parsing a number of networks and taz (district) files with shapes this script writes a taz file with all the edges which are inside the relevant taz. The taz files must be in the format generated by [POLYCONVERT](/POLYCONVERT "wikilink").

` ``/tools/edgesInDistricts.py -n myNet.net.xml -t myDistricts.rou.xml`

Call option for additional details.

filterDistricts.py
------------------

Filter a taz (district) file using a network file and a vehicle class so that only edges which allow the given vehicle class are included in the taz definitions.

` ``/tools/district/filterDistricts.py -n myNet.net.xml -t myDistricts.add.xml -o filteredDistricts.add.xml --vclass passenger`

Call option for additional details.

generateBidiDistricts.py
------------------------

Finds edges that are opposites of each other and puts them in a common district (TAZ). This can be used to improve routing in conjunction with [trip attributes fromTaz and toTaz](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Traffic_assignement_zones_.28TAZ.29 "wikilink").

` ``/tools/generateBidiDistricts.py myNet.net.xml `

Call option for additional details.

### Example usage

When applied to a typical OSM network, and edge and the edge with the negated id describe opposite direction edges of the same road. The generated bidi-taz would look like this:

` `<taz id="-123" edges="-123 123"/>
` `<taz id="123" edges="-123 123"/>

The definitions that would typically use attributes *from* and *to* instead use the attributes *fromTaz* and *toTaz*:

` `<trip id="someTrip" from="123" to="456" depart="0"/>
` `<trip id="someTripWithBidiTaz fromTaz="123" toTaz="456"/>

The second definition would allow departure from either edge *123*' or *-123*' due to the way the taz *123*' is definied. This can prevent unwanted turn-arounds and the beginning and end of generated trips and thus simplifies trips created from mapping of geo-coordinates.