---
layout: post
title: Models Emissions
permalink: /Models/Emissions/
---

__FORCETOC__

Introduction
============

SUMO includes the following emission models:

-   [HBEFA v2.1-based](/Models/Emissions/HBEFA-based "wikilink"): A continuous reformulation of the [HBEFA](http://www.hbefa.net/) v2.1 emissions data base (open source);
-   [HBEFA v3.1-based](/Models/Emissions/HBEFA3-based "wikilink"): A continuous reformulation of the [HBEFA](http://www.hbefa.net/) v3.1 emissions data base (open source);
-   [PHEMlight](/Models/Emissions/PHEMlight "wikilink"), a derivation of the original [PHEM](http://www.ivt.tugraz.at/de/forschung/emissionen.html) emission model (closed source, commercial).
-   [Electric Vehicle Model](/Models/Electric#Emission_Output "wikilink"): an electricity-consumption model by [Kurczveil, T., López, P.A., Schnieder](/Models/Electric#Publications "wikilink").

Literature on the Models and their implementation can be found at [the DLR electronic library (http://elib.dlr.de/89398/)](http://elib.dlr.de/89398/).

Using Models
============

All models implement different vehicle emission classes. These classes can be assigned to vehicles by using the vehicle type attribute “<span class="inlxml">emissionClass</span>”. Available emission classes can be found within the emission model descriptions ([HBEFA v2.1-based](/Models/Emissions/HBEFA-based "wikilink"), [HBEFA v3.1-based](/Models/Emissions/HBEFA3-based "wikilink"), [PHEMlight](/Models/Emissions/PHEMlight "wikilink")). The current default model is `HBEFA3/PC_G_EU4` (a gasoline powered Euro norm 4 passenger car modeled using the HBEFA3 based model).

Pollutants covered by models
============================

<center>
| model            | pollutant / measurement |
|------------------|-------------------------|
| CO<sub>2</sub>   | CO                      |
| HBEFA v2.1-based | x                       |
| HBEFA v3.1-based | x                       |
| PHEMlight        | x                       |
||

</center>
Outputs
=======

Pollutants emitted by the simulated vehicles can be visualised using [SUMO-GUI](/SUMO-GUI "wikilink") or be written into output files, both by [SUMO](/SUMO "wikilink") and [SUMO-GUI](/SUMO-GUI "wikilink"). The following output can be used:

-   [trip information](/Simulation/Output/TripInfo "wikilink"): In combination with the emissions device, the tripinfo output contains the sum of all pollutants emitted / fuel consumed during a vehicle's journey. To record emissions for all trips add the options and . Alternatively, you can configure emission recording for selected vehicles using [generic parameters](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes#Devices "wikilink").
-   [edgelane emissions](/Simulation/Output/Lane-_or_Edge-based_Emissions_Measures "wikilink"): These output files contain the pollutants emitted at an edge / a lane, aggregated over a variable time span
-   [Color vehicles by emissions](/SUMO-GUI#Vehicle_Visualisation_Settings "wikilink"): This can be used to show the emissions for each vehicle during each simulation step
-   [Color lanes/edges by emissions](/SUMO-GUI#Edge.2FLane_Visualisation_Settings "wikilink"): This can be used to show the emissions for all vehicles on a lane during each simulation step (or for the whole edge in [Simulation/Meso](/Simulation/Meso "wikilink")).

Further Interfaces
==================

The tool [traceExporter.py](/Tools/TraceExporter "wikilink") converts SUMO's [fcd-output](/Simulation/Output/FCDOutput "wikilink") into files that can be directly read by the [PHEM](http://www.ivt.tugraz.at/de/forschung/emissionen.html) application. A [tutorial on generating trace files (including PHEM input files)](/Tutorials/Trace_File_Generation "wikilink") using this tool is available.