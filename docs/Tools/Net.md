---
title: Tools Net
permalink: /Tools/Net/
---

netdiff.py
==========

This script compares two *.net.xml* files. The call

` ``/tools/net/netdiff.py A.net.xml B.net.xml diff`

will produce 4 [plain-XML network](/Networks/Building_Networks_from_own_XML-descriptions "wikilink") files

-   diff.nod.xml
-   diff.edg.xml
-   diff.con.xml
-   diff.tll.xml

These files contain groups of xml elemens (i.e. nodes) that have been delete, created or modified and can be used to investigate differences between the two networks *A* and *B*. Furthermore these files be used to maintain change-sets for making repeatable modifications:

`netconvert --sumo-net-file A.net.xml -n diff.nod.xml -e diff.edg.xml -x diff.con.xml -i diff.tll.xml -o B.net.xml`

The above call can be used to recreate network *B* based on *A* and the recorded change-set. Note, that for any modified elements (i.e. modified speed limit for an edge) the file *diff.edg.xml* only contains to modified attributes.

A typical use case for *netdiff.py* is this:

1.  [Import a network from OSM](/Networks/Import/OpenStreetMap "wikilink") (call this *A.net.xml*)
2.  make some modifications with [NETEDIT](/NETEDIT "wikilink") (save this under the new name *B.net.xml*)
3.  use *netdiff.py* to create the *diff*-files
4.  At a later date, re-import the OSM network (with a newer OSM file, a new version of [NETCONVERT](/NETCONVERT "wikilink") or different options)
5.  re-apply the *diff*-files to avoid repeating manual corrections with [NETEDIT](/NETEDIT "wikilink")

createRoundaboutConnections.py
==============================

This script generates additional connections for roundabouts from a given network. The following connections are added:

-   vehicles can stay inside of the roundabout on every lane.
-   vehicles can leave a roundabout even if they are driving on an inner lane if there are enough outgoing lanes.

netcheck.py
===========

This tool checks the network (first parameter) for weak connectivity (whether there is a route from every node to every other node, regardless of edge direction) and prints the connected components if not.

Additionally you may run this script to discover which edges are reachable from a particular edge

` ``/tools/net/netcheck.py <your.net.xml> --source `<edge_id>` --selection-output selection.txt`

This will create a file called *selection.txt* which can be loaded in [SUMO-GUI](/SUMO-GUI "wikilink") to visualize the portion of the network reachable from <edge_id>. To visualize the selection you must load the file using the menus **Edit-&gt;Edit chosen**. Then you need to enable edge coloring by selection status in the view settings dialog **Street-&gt;Color by: selection**. The reachable portion of the network will be colored differently from the unreachable portion which is usually sufficient to figure out network modelling errors.

The options can be shortened to for source edges and for selection output.

Using option , or , lists edges which can reach the given edge. By adding the option , or , the check becomes [vClass](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Abstract_Vehicle_Class "wikilink") aware.

The option , or , writes all the identified components and their constituent edges to the specified file. The option , or , writes the whole network summary of largest component percentage coverage and component edge count distribution to the specified file.

The and options are not compatible with the or .

Use the option for the latest version information.

netextract.py
=============

This tool extracts nodes and edges from a given network for their reuse in NETCONVERT.

xmledges_applyOffset.py and xmlnodes_applyOffset.py
=====================================================

Both tools apply the given offset to the geometrical information of edges or nodes given in the input file. The results are written into <XMLEDGES>.mod.xml or <XMLNODES>.mod.xml, respectively.

`xmledges_applyOffset.py `<XMLEDGES>` `<X-OFFSET>` `<Y-OFFSET>
`xmlnodes_applyOffset.py `<XMLNODES>` `<X-OFFSET>` `<Y-OFFSET>

-   <XMLEDGES>/<XMLNODES>: The edges/nodes file which content shall be shited
-   <X-OFFSET>: The x-offset to apply
-   <Y-OFFSET>: The x-offset to apply

xmlconnections_mapEdges.py
===========================

Reads edge id replacements from “edgemap.txt”; the format of this file is

<OLD_EDGE_ID>`->`<NEW_EDGE_ID>

Reads the given connections file <CONNECTIONS> and replaces old edge names by new. The result is written to <CONNECTIONS>.mod.xml

`xmlconnections_mapEdges.py `<CONNECTIONS>

-   <OLD_EDGE_ID>: Id of an edge as used within <CONNECTIONS>
-   <NEW_EDGE_ID>: Id of the edge as to use instead
-   <CONNECTIONS>: The connections file to change
