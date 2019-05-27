---
title: Tutorials Import from OpenStreetMap
permalink: /Tutorials/Import_from_OpenStreetMap/
---

[thumb|400px|Overview of the steps: Make up the map, compile an edge type file, and generate the SUMO network file.](/Image:OpenStreetMapOverview.svg "wikilink") OpenStreetMap is a valuable source for real-world map data. This tutorial shows you

1.  how to prepare a map of OpenStreetMap to be useful for traffic simulation and
2.  how to import this map to SUMO.

You may also find the following pages useful: [OpenStreetMap file](/OpenStreetMap_file "wikilink"), [Networks/Import/OpenStreetMap](/Networks/Import/OpenStreetMap "wikilink") and [Networks/Import/OpenStreetMapDownload](/Networks/Import/OpenStreetMapDownload "wikilink").

Prepare the Map of OpenStreetMap
--------------------------------

[thumb|400px|The OpenStreetMap file created in this step. It shows the German city Eichstätt opened in JOSM.](/Image:eichstaett.osm.png "wikilink") The first step in this tutorial is to obtain a map the vehicles can drive in. If you do not want to perform this step, you can take [Tutorials/OSMActivityGen/eichstaett.osm](/Tutorials/OSMActivityGen/eichstaett.osm "wikilink"). It has been prepared with this tutorial.

To get a detail out of OpenStreetMap, you can either use the export function of the web site or the program JOSM. Both can save a selection of objects (usually given as a rectangular range) into a file: the [OpenStreetMap file](/OpenStreetMap_file "wikilink"). You can simply use this file as the map for your traffic simulation with SUMO.

The data in OpenStreetMap is often not completely ready for traffic simulation though. For a good simulation, the map must usually be enhanced. I recommend you to do the following steps:

1.  Complete the map directly in OpenStreetMap. Follow the guidelines on the [OpenStreetMap wiki](http://wiki.openstreetmap.org) in the area *Map Making*. They give valuable hints what software to use and how to encode all attributes of the map. You should ensure that the map contains all data related to traffic simulation. (At this stage, fill in only correct data that can be well understood by others. Do not tweak the map just for your simulation. This comes below.)
    For the given example of the city Eichstätt, I found that most streets were already in the map – they were sufficient for my simulation. So I did only look at the tags (description of properties) of the streets in OpenStreetMap and did not add new streets. I took a notebook with the OpenStreetMap editor JOSM, drove through the city and corrected the following attributes:

    -   The type (importance) of a street is defined with the tag *highway*. This attribute helps SUMO to determine the implicit speed limit and right of way rule.
    -   All streets with speed limits that differ from the implicit regulatory limits (i.e. speed limits set by traffic signs) should have a tag *maxspeed*. The correct speed limits help SUMO to find reasonable routes through the road network.
    -   One-way streets often have a significant impact on the traffic flow. They can be marked in OpenStreetMap with the key-value pair *oneway=yes*.
    -   The correct number of lanes helps to avoid unrealistic traffic congestions in the simulation. The tag *lanes* specifies the total number of lanes of a street, for both directions together. So you cannot describe various complex lane configurations in OpenStreetMap (like two lanes in one direction, another lane for turning right and one lane for the opposite direction). They can only be defined in the [SUMO network file](/Networks/SUMO_Road_Networks "wikilink") directly or its corresponding [SUMO XML description files](/Networks/Building_Networks_from_own_XML-descriptions "wikilink"). Such lane configurations go beyond this tutorial.
    -   In OpenStreetMap, traffic lights are nodes marked with the key-value pair *highway=traffic_signals*. Each traffic light is independent; you cannot associate several interdependent traffic lights at a big junction with each other. Again the [SUMO network file](/Networks/SUMO_Road_Networks "wikilink") can contain such a complex logic and netconvert tries to detect such interdependent traffic lights when you use the option --try-join-tls (see section [\#Convert the Map in the SUMO Net Format](/#Convert_the_Map_in_the_SUMO_Net_Format "wikilink") below).
    -   Finally go through the warnings of JOSM. Most of them do not affect your work, but some of them help you to find significant errors in the map (like unconnected streets).

    During this step, do regularly upload your modifications to OpenStreetMap to avoid conflicts with the modifications of other editors.

2.  Now the map in OpenStreetMap should have the necessary quality for your simulation. Next you should determine the desired detail of the map and export it in an [OpenStreetMap file](/OpenStreetMap_file "wikilink"). Be careful to never upload the map back to OpenStreetMap from now on.
3.  Finally you can enhance the map for your specific purpose: Open the OpenStreetMap file in JOSM. Find the right nodes at which streets should end and remove unnecessary objects (which are out of the desired detail). The section [Networks/Import/OpenStreetMap\#Editing OSM networks](/Networks/Import/OpenStreetMap#Editing_OSM_networks "wikilink") describes further ways to clean up the OSM file. But actually, most clean up is done by netconvert anyway (see section [\#Convert the Map in the SUMO Net Format](/#Convert_the_Map_in_the_SUMO_Net_Format "wikilink") below). You are able to tweak the map for your purpose, for example, by adding or removing roads, changing their type, …

Now you have a good map for your simulation in an [OpenStreetMap file](/OpenStreetMap_file "wikilink"). The image on the top shows the map of the city Eichstätt, which I have prepared for traffic simulation. You can [download the map (eichstaett.osm)](/Tutorials/OSMActivityGen/eichstaett.osm "wikilink") to follow this tutorial.

While the OpenStreetMap format is a widely spread format to describe a map, SUMO has its own format for this: the [SUMO network format](/Networks/SUMO_Road_Networks "wikilink"). As a consequence, you must first convert the OpenStreetMap file in a SUMO network file. The next two steps guide you through the conversion process.

Configure Implicit Attributes of the Map
----------------------------------------

In a [OpenStreetMap file](/OpenStreetMap_file "wikilink"), the highway attribute implicitly determines values of some other attributes, like the speed limit. You must tell SUMO these implicit values in the [SUMO edge type file](/SUMO_edge_type_file "wikilink"). It assigns default values to the road attributes speed limit, number of lanes, priority, one-way street and allowed vehicle classes depending on the highway type. The article [SUMO edge type file](/SUMO_edge_type_file "wikilink") provides several pre-defined SUMO edge type files and explains how you can compile your own edge type file.

So determine in this step of the tutorial the implicit values of every highway type as defined by the OpenStreetMap community. Check whether one of the template in [SUMO edge type file](/SUMO_edge_type_file "wikilink") meets your needs or compile your own file. For this tutorial, I used the template . Please make a copy to your local directory if you want to modify it.

Convert the Map in a SUMO Network
---------------------------------

You can now create a [SUMO network file](/Networks/SUMO_Road_Networks "wikilink"). To do so, call

    netconvert --xml-type-files osmNetconvertUrbanDe.typ.xml --osm-files eichstaett.osm --output-file eichstaett.net.xml

netconvert extracts the simulation-related information from the OpenStreetMap file (see the image of [Tutorials/OSMActivityGen/eichstaett.osm](/Tutorials/OSMActivityGen/eichstaett.osm "wikilink") above) and puts it out in the SUMO network file (see the image of [Tutorials/OSMActivityGen/eichstaett.net.xml](/Tutorials/OSMActivityGen/eichstaett.net.xml "wikilink") below). During this process, it adds some assumptions about the traffic lights and the connections between lanes at junctions. You can read further information on this process in [NETCONVERT](/NETCONVERT "wikilink"), [Networks/Import/OpenStreetMap](/Networks/Import/OpenStreetMap "wikilink") and [SUMO Road Networks](/Networks/SUMO_Road_Networks "wikilink").

[thumb|400px|The map stored in the file eichstaett.net.xml. In this map, SUMO runs its simulation. Compare it with its source, the OpenStreetMap file shown in the image above.](/Image:eichstaett.net.png "wikilink") I found the following options of netconvert to be very useful for the OpenStreetMap import:

--guess-ramps : Guesses ramps for highways at junctions with two incoming and one outgoing road.
--remove-edges.by-vclass : In the SUMO edge type file, you could discard roads of a certain type. In addition, SUMO can discard roads that are restricted to certain vehicle classes. These classes are given with this option. In [SUMO edge type file](/SUMO_edge_type_file "wikilink") you can find a list of SUMO vehicle classes.
--remove-geometry : Removes unnecessary nodes. These are nodes without incoming/outgoing edges or nodes that split edges without being at a junction. (In OpenStreetMap, nodes are necessary to make up the shape of a street; in the SUMO network file, they are only necessary at junctions.) Warning: This could remove roads you would like to keep. So check the messages of netconvert.
--remove-isolated : Removes roads that are not connected to the remaining network. This option helps to find errors in the OSM file (unconnected roads). Warning: This could remove roads you would like to keep. So check the messages of netconvert.
--try-join-tls : Clusters junctions with traffic lights and joins the traffic light logic if possible.
--verbose : Prints additional output. Some find it useful, others find it confusing.

So the options --guess-ramps and -try-join-tls are useful here because the OpenStreetMap file misses some information necessary for traffic simulation. netconvert tries to guess this information when these options are given. --remove-isolated provides warnings that help to find a certain error in the OpenStreetMap file. --remove-geometry cleans up the nodes in the resulting SUMO network file. So does --remove-edges.by-vclass in case you want to simulate the traffic for certain vehicle classes only.

Alltogether I used the following command line to derive the SUMO network file [Tutorials/OSMActivityGen/eichstaett.net.xml](/Tutorials/OSMActivityGen/eichstaett.net.xml "wikilink") from OpenStreetMap file [Tutorials/OSMActivityGen/eichstaett.osm](/Tutorials/OSMActivityGen/eichstaett.osm "wikilink"). (It contains so many options that you might use a configuration file for it.)

    netconvert --xml-type-files osmNetconvertUrbanDe.typ.xml --guess-ramps --remove-edges.by-vclass hov,taxi,bus,delivery,transport,lightrail,cityrail,rail_slow,rail_fast,motorcycle,bicycle,pedestrian --geometry.remove --remove-edges.isolated --try-join-tls --verbose --osm-files eichstaett.osm --output-file eichstaett.net.xml

Now read the messages netconvert printed out very carefully. Try to understand the warnings. They give you a hint how your OpenStreetMap file could be improved to make it suitable for conversion. Get back to your OpenStreetMap file in JOSM to fix errors or tweak the map for conversion. I found, for example, unconnected roads with this process. I also moved some junctions slightly, because netconvert had problems if two junctions are very close together. But finally, I managed to convert the OpenStreetMap file without any warnings in a SUMO network file. (Certainly the OpenStreetMap file eichstaett.osm I provided above is already the improved version.)

*Congratulations! When you performed all the steps so far, you have a map suitable for traffic simulation with SUMO.* It is in the [SUMO network format](/Networks/SUMO_Road_Networks "wikilink"). The map of the tutorial's example is in the file [Tutorials/OSMActivityGen/eichstaett.net.xml](/Tutorials/OSMActivityGen/eichstaett.net.xml "wikilink"). Above on the right, you see an image that visualises the file. I opened eichstaett.net.xml with the program sumo-gui and took a screenshot.

When you look back at the work you have done so far, most of it was necessary to polish the OpenStreetMap data for traffic simulation and to add missing information. A good map is hard to obtain but very important for traffic simulation.