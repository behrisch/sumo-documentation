---
layout: post
title: Networks Elevation
permalink: /Networks/Elevation/
---

Including Elevation Data in a Network
=====================================

Elevation data can be imported from the following sources

-   directly from [OSM](/Networks/Import/OpenStreetMap#Elevation_Data "wikilink")
-   from a shapefile mesh by using the [NETCONVERT](/NETCONVERT "wikilink") option
-   from a greyscale height-map using [NETCONVERT](/NETCONVERT "wikilink") option .
-   from [*edg.xml* files](/Networks/Building_Networks_from_own_XML-descriptions#Edge_Descriptions "wikilink") as part of the shape specification

Related Topics
==============

Retrieving Elevation data via [TraCI](/TraCI "wikilink")
--------------------------------------------------------

Current 3D-Position can be retrieved for persons and vehicles.

Visualizing Elevation data
--------------------------

[SUMO-GUI](/SUMO-GUI "wikilink") and [NETEDIT](/NETEDIT "wikilink") allow coloring edges by:

-   elevation at the start of the edge
-   elevation at the start of each straight-line geometry segment for each edge
-   inclination of the whole edge
-   inclination of each straight-line geometry segment for each edge

Models that use Elevation Data
------------------------------

-   [Electric vehicle model](/Models/Electric "wikilink")
-   [PHEMLigh emission model](/Models/Emissions/PHEMlight "wikilink")
-   [carFollowModel=“KraussPS”](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Car-Following_Models "wikilink")
