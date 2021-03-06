---
layout: post
title: Geo-Coordinates
permalink: /Geo-Coordinates/
---

Geo-Referenced Networks
=======================

SUMO networks are always encoded in Cartesian coordinates (meters) and may contain geo-referencing information to allow conversion to lon,lat. By default the Cartesian coordinates use the UTM-projection with the origin shifted to so that the lower left corner of the network is at 0,0.

-   When importing a network from [OSM](/Networks/Import/OpenStreetMap "wikilink"), geo-referencing is automatically included in the generated *.net.xml* file
-   When importing a network from [plain-xml](/Networks/Building_Networks_from_own_XML-descriptions "wikilink") files, coordinates may be given in lon,lat and importing using a projection option such as
-   When importing a network from Shapefile, the availability of geo-referencing depends on the format of the source data.

Checking Geo-Coordinates
========================

In [SUMO-GUI](/SUMO-GUI "wikilink") when right-clicking anywhere in a geo-referenced network, the option *copy cursor geo-position to clipboard* is available. The resulting *lat,lon* coordinates are suitable for pasting into any map engine such as \[maps.google.com\] or \[maps.bing.com\]. Also, the network coordinates as well as the geo-coordinates at the cursor position are shown in the bottom right-corner of the window.

Performing coordinate-transformations
=====================================

-   using [TraCI](/TraCI/Simulation_Value_Retrieval#Command_0x82:_Position_Conversion "wikilink"), coordinates can be transformed between network-coordinates (m,m) and geo-coordinates (lon,lat) and vice versa
-   using [sumolib](/Tools/Sumolib#coordinate_transformations "wikilink") , coordinates can be transformed between network-coordinates (m,m) and geo-coordinates (lon,lat) and vice versa

Obtaining output with geo-coordinates
=====================================

-   A network can be exported as *plain-xml* in geo-coordinates using the netconvert command

` netconvert --sumo-net-file myNet.net.xml --plain-output-prefix plain --proj.plain-geo`

-   [FCD-output](/Simulation/Output/FCDOutput "wikilink") can be obtained in geo-coordinates by adding the option
