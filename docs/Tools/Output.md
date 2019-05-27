---
title: Tools Output
permalink: /Tools/Output/
---

All of the tools described below exist in *tools/output* directory.

generateITetrisIntersectionMetrics.py
-------------------------------------

Tool used for generating the intersection metrics, including (but not limited to):

-   CO emission
-   CO2 emission
-   HC emission
-   PMx emission
-   NOx emission
-   fuel consumption

Execute the *generateITetrisIntersectionMetrics.py* script with *--help* option to get details about usage and available options.

generateITetrisNetworkMetrics.py
--------------------------------

Tool used for generating the network metrics, including (but not limited to):

-   CO emission
-   CO2 emission
-   HC emission
-   PMx emission
-   NOx emission
-   fuel consumption

Execute the *generateITetrisINetworkMetrics.py* script with *--help* option to get details about usage and available options.

generateMeanDataDefinitions.py
------------------------------

Script for generating mean data definitions from detector definitions.

Execute the *generateITetrisINetworkMetrics.py* script with *--help* option to get details about usage and available options.

generateTLSE1Detectors.py
-------------------------

Script for generating [E1 detectors (induction loops)](/Simulation/Output/Induction_Loops_Detectors_(E1) "wikilink") for each junction in the supplied network file.

Execute the *generateTLSE1Detectors.py*script with *--help* option to get details about usage and available options.

generateTLSE2Detectors.py
-------------------------

Script for generating [E2 detectors (lanearea detectors)](/Simulation/Output/Lanearea_Detectors_(E2) "wikilink") for each junction in the supplied network file.

Execute the *generateTLSE2Detectors.py* script with *--help* option to get details about usage and available options.

generateTLSE3Detectors.py
-------------------------

Script for generating [E3 detectors (multi-entry/multi-exit detectors)](/Simulation/Output/Multi-Entry_Multi-Exit_Detectors_(E3) "wikilink") for each junction in the supplied network file.

Execute the *generateTLSE3Detectors.py* script with *--help* option to get details about usage and available options.

netdumpdiff.py
--------------

Script creating a diff of two netdump files.

Execute the *netdumpdiff.py* script with *--help* option to get details about usage and available options.

netdumpmean.py
--------------

Script calculating the mean values from two netdump files.

Execute the *netdumpmean.py* script with *--help* option to get details about usage and available options.

timingStats.py
--------------

Script for gathering statistics from several SUMO runs.

Execute the *timingStats.py* script with *--help* option to get details about usage and available options.

accelerations.py
----------------

Script for computing aggregate statistics about vehicle acclerations based on [--netstate-dump](/Simulation/Output/RawDump "wikilink") output.

vehLanes.py
-----------

Script for computing [vehroute](/Simulation/Output/VehRoutes "wikilink")-like output for lanes based on [--netstate-dump](/Simulation/Output/RawDump "wikilink") output. Output data also includes information about the number of lane changes for each vehicle.

usage:

` python vehLanes.py <netstate_dump.xml> `<output_file>

edgeDataDiff.py
---------------

Computes the numerical difference of [edgeData](/Simulation/Output/Lane-_or_Edge-based_Traffic_Measures "wikilink") values for each edge and interval. The resulting file can be used to visualize changes between two traffic scenarios. Both input files must contain the same edges and intervals.

usage:

` python edgeDataDiff.py <edgeData1.xml> <edgeData2.xml> <diffFile.xml>`

vehrouteDiff.py
---------------

Computes the difference in travel times between two sets of files. The files must contain the same vehicles and the same routes and may only differ in travel times. The must have been generated with the option for the script to work.

usage:

` python vehrouteDiff.py routes1.rou.xml routes2.rou.xml result.xml`

tripinfoDiff.py
---------------

Computes the difference in travel times, route length, time loss, departure- and arrival times between two sets of files. The files should contain the same vehicles.

usage:

` python tripinfoDiff.py tripinfos1.xml tripinfos2.xml result.xml`