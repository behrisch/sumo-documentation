---
title: Networks Further Outputs
permalink: /Networks/Further_Outputs/
---

[NETCONVERT](/NETCONVERT "wikilink"), [NETGENERATE](/NETGENERATE "wikilink"), and [NETEDIT](/NETEDIT "wikilink") allow to generate additional output files besides writing a SUMO network file. They will be presented in the following.

Writing/Exporting Networks
==========================

If no other output option is given, [NETCONVERT](/NETCONVERT "wikilink") and [NETGENERATE](/NETGENERATE "wikilink") will write the result of network import/generation as a SUMO network file into “net.net.xml”. Otherwise the specified output will be generated.

Currently, the applications allow to write networks in the following formats:

-   SUMO road networks
-   plain XML definitions, as described in [Networks/Building Networks from own XML-descriptions](/Networks/Building_Networks_from_own_XML-descriptions "wikilink")
-   MATsim networks

SUMO Road Networks
------------------

This is the default output format, see above. The name of the file to write the network into can be given using the option . and are synonymes.

Plain XML Output
----------------

Parsed node and edge definitions may be saved into a XML-files which have the same formats as the ones used for importing XML-networks (as described in [Node Descriptions](/Networks/Building_Networks_from_own_XML-descriptions#Node_Descriptions "wikilink") and [Edge Descriptions](/Networks/Building_Networks_from_own_XML-descriptions#Node_Descriptions "wikilink")). This shall ease processing of networks read from other formats than XML. The option forces [NETCONVERT](/NETCONVERT "wikilink") and [NETGENERATE](/NETGENERATE "wikilink") to generate a file named “.nod.xml” which contains the previously imported nodes, a file named “.edg.xml” which contains the previously imported edges, and a file named “.con.xml” which contains the previously imported connections. The edge file will contain the list of previously read edges and each edge will have the information about the edge's id, the allowed velocity, the number of lanes, and the from/to - nodes stored. Geometry information is stored only if the imported edge has a shape, meaning that it is not only a straight connection between the from/to-nodes. The lane spread type and the basic edge type are only saved if differing from defaults (“right” and “normal”, respectively). Additionally, if one of the lanes prohibits/allows vehicle classes, this information is saved, too (see also “Defining allowed Vehicle Types”).

MATsim Road Networks
--------------------

To write the imported/generated network as a MATsim file, use the option . The extension for MATsim networks is usually “.xml”.

Please note that the capacity is computed by multiplying an edge's lane number with the capacity norm:

`MAXIMUM_FLOW = LANE_NUMBER * CAPACITY_NORM`

The value of CAPACITY_NORM is controlled via the option (default: 1800).

OpenDRIVE Road Networks
-----------------------

To write the imported/generated network as a [OpenDRIVE](/Networks/Import/OpenDRIVE "wikilink") file (version 1.4), use the option . The extension for OpenDRIVE networks is usually “.xodr”.

Some notes:

-   The feature is currently under implementation
-   <span class="inlxml">road</span> - the normal ones
    -   the road <span class="inlxml">type</span> is always set to “<span class="inlxml">town</span>” for the complete street
    -   the lane <span class="inlxml">type</span> is set to either *biking, sidewalk, tram, none* or *driving* according to the edge permissions.
    -   <span class="inlxml">link</span>
        -   The road is always connected to the nodes it is outgoing (<span class="inlxml">predecessor</span>) / incoming (<span class="inlxml">successor</span>) from/to
    -   <span class="inlxml">planView</span>
        -   the geometry is given as lines and paramPoly3
    -   no road widenings are modeled - if the number of lanes changes, the road changes
    -   <span class="inlxml">elevationProfile</span> is written if the network contains 3D geometries
    -   <span class="inlxml">lateralProfile</span> does not contain relevant information
    -   the roads are always unidirectional, this means only the center lane and the right lanes are given
    -   <span class="inlxml">objects</span> and <span class="inlxml">signals</span> do not contain relevant information

Recommended options

-   . This elongates junction shapes to allow for smooth transitions (values around *1.0* can be used to reduced or increase stretching)

-   . This records the edge IDs from the corresponding *.net.xml* within elements as children of the

Further Outputs
===============

Public Transport Stops
----------------------

The option causes an to be written that contains elements for the imported network. These can be loaded directlyl into [SUMO](/SUMO "wikilink") or further modified with [NETEDIT](/NETEDIT "wikilink").

Information on Joined Junctions
-------------------------------

The option causes a file to be written that specifies the junctions which were joined (usualy due to option ). The resulting output file is suitable for loading with the option.

Street Signs
------------

The option causes a file with [POIs](/Simulation/Shapes#POI_.28Point_of_interest.29_Definitions "wikilink") to be written. These POIs encode the type of street signs that are encountered on each edge and can be loaded as in [SUMO-GUI](/SUMO-GUI "wikilink"). Currently used sign types are:

-   priority
-   yield
-   stop
-   allway_stop
-   right_before_left

Additional Information within the output file
---------------------------------------------

The option ensures that street names from suitable input networks such as [OSM](/Networks/Import/OpenStreetMap "wikilink") or [OpenDrive](/Networks/Import/OpenDRIVE "wikilink") are included in the generated *.net.xml* file.

When reading or writing OpenDrive networks, the option [writtes additional data for mapping between sumo-ids and OpenDrive-ids into the generated networks](/Networks/Import/OpenDRIVE#Referencing_original_IDs "wikilink").