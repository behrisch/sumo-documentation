---
title: Networks Export
permalink: /Networks/Export/
---

Supported export formats
========================

SUMO
----

The default output format, when using no other options. While being partly similar in structure to the plain format below, this file is not meant to be edited by hand since there are complex dependencies between the various parts.

Plain
-----

Generated when using the option , it generates four files containing the nodes, the edges, the connections and the traffic light logics as described in [Networks/Building_Networks_from_own_XML-descriptions](/Networks/Building_Networks_from_own_XML-descriptions "wikilink").

OpenDRIVE
---------

The option writes networks in the [OpenDRIVE](/Networks/Import/OpenDRIVE "wikilink") format adhering to version 1.3.

MATsim
------

The creates MATsim networks.

DlrNavteq
---------

The generates a links, a nodes and a traffic lights file matching extraction version 6.0.

Amitran
-------

The Amitran network format consists of a single XML file conforming to the schema at <http://sumo-sim.org/xsd/amitran/network.xsd>. The option writes the data to a file with the following format

<?xml version="1.0" encoding="utf-8"?>
<network xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://sumo-sim.org/xsd/amitran/network.xsd">
`   `<node id="0" type="rightBeforeLeft"/>
`   `<node id="1" type="priority"/>
`   ...`
`   `<link id="0" from="1" to="0" roadClass="4" length="136448" speedLimitKmh="20" laneNr="1"/>
`   ...`
</network>

where all values are integers (the length is in units of 0.01m, the road class is a functional road class in the Navteq sense)