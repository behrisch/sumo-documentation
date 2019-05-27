---
title: Z Changes from Version 0.27.0 to Version 0.27.1
permalink: /Z/Changes_from_Version_0.27.0_to_Version_0.27.1/
---

Version 0.27.1 (27.07.2016)
---------------------------

### Bugfixes

-   NETCONVERT
    -   Original IDs are no longer lost when splitting edges.
    -   Elevation data is now correctly imported from OpenDRIVE networks.

<!-- -->

-   NETEDIT
    -   Fixed crash when increasing the number of lanes by setting numLanes.
    -   Fixed slow loading of large networks.
    -   Custom colors for selected junctions and edges are now working.

<!-- -->

-   DUAROUTER
    -   Fixed crash when using option with invalid -edges.

### Enhancements

-   Simulation
    -   Added new option to save simulation state periodically.
    -   Added new option to determine the suffix of saved state files. The default is *.sbx* which saves in a binary format. Alternatively, *.xml* may be used which makes the state files human-readable.

<!-- -->

-   NETCONVERT
    -   Networks exported to OpenDRIVE now use parametric curves to represent smooth geometry in place of straight-line segments.
    -   Networks exported to OpenDRIVE now contain elevation data.
    -   Parametric curves as specified in OpenDRIVE version 1.4 can now be imported.
    -   Revised default OpenDRIVE typemap. Now imports additional lane types such as tram and rail.
    -   Added new option to import implicit elevation data from [OSM-layering information](/Networks/Import/OpenStreetMap#Layer_Information "wikilink").
    -   Networks imported from OpenDRIVE now contain edge type information based on the OpenDRIVE lane types.

<!-- -->

-   SUMO-GUI
    -   Added Visualization options for drawing intersections with exaggerated size and disable edge drawing based on custom widths.
    -   Added Visualization option for indicating the driving direction of lanes.
    -   Added Visualization option for drawing [sublane boundaries](/Simulation/SublaneModel "wikilink")
    -   Lanes can now be colored according to the number of vehicles that are delayed from entering the network.

<!-- -->

-   NETEDIT
    -   Added Visualization options for drawing intersections with exaggerated size and disable edge drawing based on custom widths.
    -   Added Visualization option for indicating the driving direction of lanes.
