---
layout: post
title: JTRROUTER
permalink: /JTRROUTER/
---

From 30.000 feet
================

**JTRROUTER** computes routes that may be used by [SUMO](/SUMO "wikilink") based on traffic volumes and junction turning ratios.


**Purpose:** Building vehicle routes from demand definitions using junction turning percentages

**System:** portable (Linux/Windows is tested); runs on command line

**Input (mandatory):**
A) a road network as generated via [NETCONVERT](/NETCONVERT "wikilink") or [NETGENERATE](/NETGENERATE "wikilink"), see [Building Networks](/SUMO_User_Documentation#Network_Building "wikilink")

B) a demand definition, see [Demand Modelling](/SUMO_User_Documentation#Demand_Modelling "wikilink")

C) Junction turning definitions

**Output:** [Definition of Vehicles, Vehicle Types, and Routes](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes "wikilink") usable by [SUMO](/SUMO "wikilink")

**Programming Language:** C++

Usage Description
=================

JTRROUTER is made for [routing based on turn-ratios](/Demand/Routing_by_Turn_Probabilities "wikilink").

Options
-------

You may use a XML schema definition file for setting up a JTRROUTER configuration: [jtrrouterConfiguration.xsd](http://sumo.dlr.de/xsd/jtrrouterConfiguration.xsd).

### Configuration

All applications of the **SUMO**-suite handle configuration options the same way. These options are discussed at [Basics/Using the Command Line Applications\#Configuration Files](/Basics/Using_the_Command_Line_Applications#Configuration_Files "wikilink").

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
<td><p>Loads the named config on startup</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Saves current configuration into FILE</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Saves a configuration template (empty) into FILE</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Saves the configuration schema into FILE</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Adds comments to saved template, configuration, or schema; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

### Input

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
<td><p>Use FILE as SUMO-network to route on</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Read additional network data (districts, bus stops) from FILE(s)</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Read sumo routes, alternatives, flows, and trips from FILE(s)</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Read turning ratios from FILE(s)</p></td>
</tr>
<tr class="odd">
</tr>
</tbody>
</table>

### Output

<table>
<thead>
<tr class="header">
<th><p>Option</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td></td>
<td><p>Prefix which is applied to all output files. The special string 'TIME' is replaced by the current time.</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Defines the number of digits after the comma for floating point output; <em>default: <strong>2</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Defines the number of digits after the comma for lon,lat output; <em>default: <strong>6</strong></em></p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Write generated routes to FILE</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Write used vehicle types into separate FILE</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Keep vTypeDistribution ids when writing vehicles and their types; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Write exit times (weights) for each edge; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

### Processing

<table>
<thead>
<tr class="header">
<th><p>Option</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td></td>
<td><p>Continue if a route could not be build; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Assume input is unsorted; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Load routes for the next number of seconds ahead; <em>default: <strong>200</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>generate random departure times for flow input; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Prune the number of alternatives to INT; <em>default: <strong>5</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Remove loops within the route; Remove turnarounds at start and end of the route; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Tries to correct a false route; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Tries to correct an invalid starting edge by using the first usable edge instead; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Tries to correct an invalid destination edge by using the last usable edge instead; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Interpolate edge weights at interval boundaries; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Use origin and destination zones (districts) for in- and output; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Aggregate routing queries with the same origin; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>The number of parallel execution threads used for routing; <em>default: <strong>0</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Routes are cut off when the route edges to net edges ratio is larger than FLOAT; <em>default: <strong>2</strong></em></p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Use STR as default turn definition; <em>default: <strong>30,50,20</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Use STR as list of sink edges</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Whether all edges are allowed as sink edges; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Ignore road restrictions based on vehicle class; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Allow to re-use a road; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

### Defaults

| Option | Description                                               |
|--------|-----------------------------------------------------------|
|        | Assigns a default depart lane                             |
|        | Assigns a default depart position                         |
|        | Assigns a default depart speed                            |
|        | Assigns a default arrival lane                            |
|        | Assigns a default arrival position                        |
|        | Assigns a default arrival speed                           |
|        | Defaults will override given values; *default: **false*** |
||

### Time

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
<td><p>Defines the begin time; Previous trips will be discarded; <em>default: <strong>0</strong></em></p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Defines the end time; Later trips will be discarded; Defaults to the maximum time that SUMO can represent; <em>default: <strong>9223372036854774</strong></em></p></td>
</tr>
<tr class="odd">
</tr>
</tbody>
</table>

### Report

All applications of the **SUMO**-suite handle most of the reporting options the same way. These options are discussed at [Basics/Using the Command Line Applications\#Reporting Options](/Basics/Using_the_Command_Line_Applications#Reporting_Options "wikilink").

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
<td><p>Switches to verbose output; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Prints option values before processing; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Prints this screen; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Prints the current version; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Set schema validation scheme of XML inputs (“never”, “auto” or “always”); <em>default: <strong>auto</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Set schema validation scheme of SUMO network inputs (“never”, “auto” or “always”); <em>default: <strong>never</strong></em></p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Disables output of warnings; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Writes all messages to FILE (implies verbose)</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Writes all non-error messages to FILE (implies verbose)</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Writes all warnings and errors to FILE</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Defines how often statistics shall be printed; <em>default: <strong>-1</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Disable console output of route parsing step; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
</tr>
</tbody>
</table>

### Random Number

All applications of the **SUMO**-suite handle randomisation options the same way. These options are discussed at [Basics/Using the Command Line Applications\#Random Number Options](/Basics/Using_the_Command_Line_Applications#Random_Number_Options "wikilink").

| Option | Description                                                                                |
|--------|--------------------------------------------------------------------------------------------|
|        | Initialises the random number generator with the current system time; *default: **false*** |
|        | Initialises the random number generator with the given value; *default: **23423***         |
||

------------------------------------------------------------------------

[Category:ApplicationDescription](/Category:ApplicationDescription "wikilink")