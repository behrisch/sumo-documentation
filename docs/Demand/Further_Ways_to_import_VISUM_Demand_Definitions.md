---
layout: post
title: Demand Further Ways to import VISUM Demand Definitions
permalink: /Demand/Further_Ways_to_import_VISUM_Demand_Definitions/
---

VISUM stores its demand in [OD-matrices which can be imported](/Demand/Importing_O/D_Matrices "wikilink") using [OD2TRIPS](/OD2TRIPS "wikilink"). Though, it may be interesting for using the computed assignments without performing a [dynamic user assignment](/Demand/Dynamic_User_Assignment "wikilink"). The SUMO package contains some scripts which allow to process other VISUM data and are discussed in the following.

Importing Turn Percentages
==========================

VISUM can save the defined/computed turning percentages at junctions. The format differs from [turning probabilities format](/Demand/Routing_by_Turn_Probabilities "wikilink") used by [JTRROUTER](/JTRROUTER "wikilink"). The script ***visum_convertTurnPercentages.py*** converts VISUM turning percentages into [JTRROUTERs](/JTRROUTER "wikilink") [turning definitions](/Demand/Routing_by_Turn_Probabilities "wikilink"). The tool requires the SUMO-network converted from VISUM, the turning probabilities from VISUM, and the name of the file into which the converted turning probabilities shall be written:

`visum_convertTurnPercentages.py `<SUMO_NET>` `<VISUM_TURNINGS>` `

<OUTPUT>
The script is located in /tools/import/visum. It is written in Python.

Usability
---------

It seems as using turning ratios for large areas would not make any sense. The resulting routes are very unrealistic as they contain many loops.

See Also
--------

-   [JTRROUTER](/JTRROUTER "wikilink") - page on the turning ratios router
-   [Demand/Routing by Turn Probabilities](/Demand/Routing_by_Turn_Probabilities "wikilink") - further documentation on this tool's usage

Importing Routes
================

VISUM can save the routes it computes during the assignment. The format differs from [Definition of Vehicles, Vehicle Types, and Routes](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes "wikilink") used by [SUMO](/SUMO "wikilink") and [SUMO-GUI](/SUMO-GUI "wikilink"). The script ***visum_convertRoutes.py*** converts VISUM routes into [SUMO](/SUMO "wikilink") routes. The tool requires the SUMO-network converted from VISUM, the routes exported from VISUM, and the name of the file into which the converted turning probabilities shall be written. Additional options are shown in the following table:

<table>
<thead>
<tr class="header">
<th><p>Option</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Read the SUMO-network to map the routes onto from <FILE>; mandatory</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Read VISUM-routes to map from <FILE>; mandatory</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Write generated routes to <FILE>; mandatory</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Define the begin of the interval the vehicles are emitted within [s]; default: 0s</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Define the end of the interval the vehicles are emitted within [s]; default: 3600s</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Add <STRING> as prefix to the IDs of generated vehicles; optional, default: no prefix</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Set the vehicle type to <STRING>; optional, default: no type</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Vehicle departure times will be spread across the interval uniformly; optional, default: false</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Applies a daily time line. The time line must be given as a list of 24 floats, each describing the percentage of emissions from the original number for each hour of a day; optional, default: no timeline</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

Example call:

`visum_convertRoutes.py -n `<SUMO_NET>` -r `<VISUM_ROUTES>` -o `

<OUTPUT>
--uniform The script is located in /tools/import/visum. It is written in Python.

Usability
---------

The routes can be directly used within [SUMO](/SUMO "wikilink") / [SUMO-GUI](/SUMO-GUI "wikilink").

See Also
--------

-   [Examples of daily time lines](/Demand/Importing_O/D_Matrices#Daily_Time_Lines "wikilink")
