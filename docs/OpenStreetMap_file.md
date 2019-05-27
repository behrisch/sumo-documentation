---
title: OpenStreetMap file
permalink: /OpenStreetMap_file/
---

[thumb|400px|The screenshot of an OpenStreetMap file opened in JOSM. It shows the map of the German city Eichstätt.](/Image:eichstaett.osm.png "wikilink") An **OpenStreetMap file** contains an extract of the OpenStreetMap database. The data is saved in an XML structure. The file name typically ends with .osm or .osm.xml.

You can get an OpenStreetMap file in various ways. The page [Networks/Import/OpenStreetMapDownload](/Networks/Import/OpenStreetMapDownload "wikilink") explains them.

In the context of SUMO, an OpenStreetMap file can provide the map for the traffic simulation. It serves as the basis for a [SUMO network file](/Networks/SUMO_Road_Networks "wikilink"). The pages [Networks/Import/OpenStreetMap](/Networks/Import/OpenStreetMap "wikilink") and [Tutorials/Import from OpenStreetMap](/Tutorials/Import_from_OpenStreetMap "wikilink") show how to convert an OpenStreetMap file to a SUMO network file.

Traffic Simulation Related Content
----------------------------------

An OpenStreetMap file contains a map with the following features related to traffic simulation:

-   The nodes and their connections define the position and form of all streets and junctions.
-   The type of a street specifies its size and importance (key *highway*).
-   The speed limit of a street is usually determined implicitly by law. The implicit value may depend on the value of the highway attribute. In case, the speed limit differs from the implicit legal value, it is given explicitly through the key *max_speed* of a street.
-   The total number of lanes (for both directions) has an implicit value depending on the highway property. If the real value differs from the default value, it can be given through the key *lanes*.
-   The position of every traffic light is described as a node with the key-value pair *highway=traffic_signals*.
-   One-way streets are marked with the key-value pair *oneway=yes*.

Compared with the [SUMO network file](/Networks/SUMO_Road_Networks "wikilink") format, the OpenStreetMap file format lacks in

-   The logic of the traffic lights and
-   The meaning of lanes and the connections between lanes at a junction.

Software for Viewing, Editing and Processing
--------------------------------------------

The OpenStreetMap wiki lists [a few tools to process OpenStreetMap files](http://wiki.openstreetmap.org/wiki/Category:OSM_processing). As a graphical editor, **[JOSM](http://josm.openstreetmap.de/)** is very popular. You can modify roads and tags with it and also run some validation checks. The command line editor **[Osmosis](http://wiki.openstreetmap.org/wiki/Osmosis)** allows automated processing of OpenStreetMap data (see, for example, [Networks/Import/OpenStreetMap\#Editing OSM networks](/Networks/Import/OpenStreetMap#Editing_OSM_networks "wikilink")).

To use the map in the OpenStreetMap file with SUMO, you must convert it in a [SUMO network file](/Networks/SUMO_Road_Networks "wikilink"). Typically you do this with **[NETCONVERT](/NETCONVERT "wikilink")** (see also [Tutorials/Import from OpenStreetMap](/Tutorials/Import_from_OpenStreetMap "wikilink") and [Networks/Import/OpenStreetMap](/Networks/Import/OpenStreetMap "wikilink")). You could also use **[eWorld](http://eworld.sourceforge.net)** to manipulate a OpenStreetMap file and convert it in a SUMO network file.