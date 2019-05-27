---
layout: post
title: Tutorials ScenarioGuide
permalink: /Tutorials/ScenarioGuide/
---

Introduction
============

This Tutorial is meant to serve as a high-level guide for building a [SUMO](/SUMO "wikilink") scenario. It provides an outline of the typical steps when building a scenario and lists the recommended wiki pages for each step.

Build the road network
======================

Every simulation requires a road network. The application [NETCONVERT](/NETCONVERT "wikilink") is used to create a network which can be used by the simulation [SUMO](/SUMO "wikilink").

If you already have some network data
-------------------------------------

Check whether a direct import is possible: [Networks/Import](/Networks/Import "wikilink"). Otherwise you will need to convert the data to a simple XML-format which can be read by [NETCONVERT](/NETCONVERT "wikilink"). Read this page: [Networks/Import](/Networks/Import "wikilink").

If you do not yet have any network data
---------------------------------------

Use publicly available network data from [OpenStreetMap](http://www.openstreetmap.org/) as described here: [Networks/Import/OpenStreetMapDownload](/Networks/Import/OpenStreetMapDownload "wikilink"). Then import the network as described here: [Networks/Import/OpenStreetMap](/Networks/Import/OpenStreetMap "wikilink").

Generate the traffic
====================

First you should understand the basics of vehicle modelling: [Definition_of_Vehicles,_Vehicle_Types,_and_Routes](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes "wikilink"). You have various ways to insert vehicles into the map. Your choice basically depends on what kind of information about the traffic you have: [Demand/Introduction_to_demand_modelling_in_SUMO](/Demand/Introduction_to_demand_modelling_in_SUMO "wikilink").

Improve your Scenario
=====================

Most methods for network import leave some aspect of deficient network quality. Very often this manifests as unexpected/unrealistic traffic jams and teleporting vehicle errors.

Modifying the Network
---------------------

You will have to patch your network data to add missing roads, prohibit some turns, correct the number of lanes and add/remove some traffic lights. The recommended way to perform the necessary changes is this:

1.  Encode the changes in *plain-xml* files as described in [Networks/Building_Networks_from_own_XML-descriptions](/Networks/Building_Networks_from_own_XML-descriptions "wikilink"). Most XML-attributes are optional so you only need to set the values you would like to change.
2.  patch your network using [NETCONVERT](/NETCONVERT "wikilink") by loading the net.xml along with the plain-xml files. You can even use this during the initial import (i.e. load an OSM-file along with your plain-xml files)

### Example: Patching the type of a node

prepare a file like this:

patch.nod.xml :

` `<nodes>
`    `<node id="id_of_the_node_you_want_to_modify" type="right_before_left"/>
` `<nodes>

and patch the network like this:

` netconvert --sumo-net-file your.net.xml --node-files patch.nod.xml -o yourpatched.net.xml`

or perform the patch during the initial import:

`netconvert --osm-file yourOSMfile.xml --node-files patch.nod.xml ...`<other options>

### Modifying an imported network via plain.xml

Instead of patching individual elements you can also convert your network to plain.xml and modify the plain file and then re-assemble the network like this:

` netconvert --sumo-net-file your.net.xml --plain-output-prefix yourplain`

or during import:

` netconvert --osm-files yourOSMinput.xml --plain-output-prefix yourplain ... `<your other options>

This will give you the files:

` yourplain.edg.xml`
` yourplain.nod.xml`
` yourplain.con.xml`
` yourplain.tll.xml`

You can edit these files and then reassamble the network buy loading some or all of them:

` netconvert --edge-files yourplain.edg.xml --node-files yourplain.nod.xml -o new.net.xml`

or

` netconvert --edge-files yourplain.edg.xml --node-files yourplain.nod.xml --connection-files yourplain.con.xml -o new.net.xml`

Traffic Light Programs
----------------------

In almost all cases the traffic light programs will have been guessed by [NETCONVERT](/NETCONVERT "wikilink") and turn out different from the real traffic lights. A simple way to improve traffic lights programs is making them start their program cycle at a different time. Experiment with the option and all the other options of [NETCONVERT](/NETCONVERT "wikilink").

A more powerful way to improve your traffic lights is to [give the program explicitly with a *tls.xml* file](/Networks/Building_Networks_from_own_XML-descriptions#Traffic_Light_Program_Definition "wikilink").

At this time [NETCONVERT](/NETCONVERT "wikilink") only supports the creation of static traffic light programs. For dynamic traffic lights see [Tutorials/TraCI4Traffic_Lights](/Tutorials/TraCI4Traffic_Lights "wikilink").

Manage Scenarios
================

If you have two networks *A.net.xml* and *B.net.xml* you may wish to find out how they differ. This can be accomplished using the tool */tools/net/netdiff.py*. Running this tool will give you a set of plain-XML difference files. They only contain the differences grouped by *deleted*, *created* and *changed* elements. It is even possible to load these files along with *A.net.xml* to recreate *B.net.xml*.