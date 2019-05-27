---
title: Z Changes from Version 0.13.0 to Version 0.13.1
permalink: /Z/Changes_from_Version_0.13.0_to_Version_0.13.1/
---

**Release Date: 01.11.2011**

### Bugfixes

-   switched-off traffic lights are now put into the correct state
-   vehicles with gui shape can now be used as router input
-   updated tutorial networks
-   fixed bug in duarouter which prevented use of multiple inline routes
-   object-chooser no longer centers on unwanted objects

### Enhancements

-   TraCI
    -   Added the possibility to retrieve an induction loop's position (offset/lane) as suggested by Xiao-Feng Xie; thanks!
    -   Added the possibility to [remove a vehicle via TraCI](/TraCI/Change_Vehicle_State "wikilink")
    -   Added the description about how to [add a vehicle via TraCI](/TraCI/Change_Vehicle_State "wikilink")
    -   Retrieve the number of still expected vehicles
-   NETCONVERT
    -   added more control over joining junctions. You can declare nodes to be joined as well as exclude nodes from joining (see [Networks/Building_Networks_from_own_XML-descriptions\#Joining_Nodes](/Networks/Building_Networks_from_own_XML-descriptions#Joining_Nodes "wikilink"))
    -   added option (do not use tls definitions when importing OSM)
    -   added option (junctions in this list are not joined)
    -   added option (do not build connections to left)
    -   added optional attributes 'toLane' and 'fromLane' to connection-file element 'reset' (see [Networks/Building_Networks_from_own_XML-descriptions\#Connection_Descriptions](/Networks/Building_Networks_from_own_XML-descriptions#Connection_Descriptions "wikilink"))
    -   added importer for openDRIVE files, see [Networks/Import/OpenDRIVE](/Networks/Import/OpenDRIVE "wikilink"); many thanks go to Marius Dupuis from [VIRES](http://www.vires.com/) for allowing to use the example files for tests
    -   added importer for matSIM files, see [Networks/Import/MATsim](/Networks/Import/MATsim "wikilink") (actually already in 0.13.0)
    -   added new plain xml input/output format **plain.tll.xml** which holds information about traffic lights.
    -   added option to restrict segment length by inserting additional geometry points
    -   debugged brakedown on VISUM import
    -   ignore connections for explicitly removed edges (instead of throwing an error)
-   Simulation
    -   Added [Simulation/Output/Instantaneous Induction Loops Detectors](/Simulation/Output/Instantaneous_Induction_Loops_Detectors "wikilink")
    -   [Simulation/Output/Induction Loops Detectors (E1)](/Simulation/Output/Induction_Loops_Detectors_(E1) "wikilink") now also allow to generate values on per-vehicle type base
-   JTRROUTER
    -   added Karol Stosiek's patch for reading more than one turn-definitions file; changes to
-   SUMO-GUI
    -   can now switch traffic lights back on
-   Tutorials
    -   moved tutorials from /docs to /tests/complex for assuring their compliance with the current version; they should though appear in the release under /docs
    -   added a [tutorial on car-following parameter calibration](/Tutorials/Calibration/San_Pablo_Dam "wikilink")
-   Tools
    -   added script tools/net/netdiff.py *&lt;net1.net.xml&gt; &lt;net2.net.xml&gt; <diff_prefix>* which creates the plain-xml differences of two sumo networks. The set of difference files can be loaded together with *&lt;net1.net.xml&gt;* to recreate *&lt;net2.net.xml&gt;*. This allows for advanced scenario management.
    -   added tools for dealing with turn-ratios
-   Documentation
    -   restructured wiki-pages
    -   new static HTML docs generated from the wiki

### Other

-   updated gl2ps to version 1.3.6
-   removed MSMsgInductLoop; the functionality was almost the same as for a plain MSInductLoop just that an additional string wasgiven; the functionality can be easily obtained by using proper ids and mapping them to “messages”
