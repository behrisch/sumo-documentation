---
title: ACTIVITYGEN
permalink: /ACTIVITYGEN/
---

From 30.000 feet
================

[ACTIVITYGEN](/ACTIVITYGEN "wikilink") reads the definition of a population matching an also given network. It computes and mobility wishes for this population.


**Purpose:** Demand generation for a synthetic population

**System:** portable (Linux/Windows is tested); runs on command line

**Input (mandatory):**
A) a road network as generated via [NETCONVERT](/NETCONVERT "wikilink") or [NETGENERATE](/NETGENERATE "wikilink"), see [Building Networks](/SUMO_User_Documentation#Network_Building "wikilink")

B) a population definition, see [Activity-based Demand Generation](/Demand/Activity-based_Demand_Generation "wikilink")

**Output:** [Definition of Vehicles, Vehicle Types, and Routes](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes "wikilink") usable by [SUMO](/SUMO "wikilink")

**Programming Language:** C++

Usage Description
=================

A step by step description for using [ACTIVITYGEN](/ACTIVITYGEN "wikilink") can be found [here](/Demand/Activity-based_Demand_Generation "wikilink")

Options
-------

You may use a XML schema definition file for setting up a ACTIVITYGEN configuration: [activitygenConfiguration.xsd](http://sumo.dlr.de/xsd/activitygenConfiguration.xsd).

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
<td><p>Use FILE as SUMO-network to create trips for</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Loads the SUMO-statistics FILE</p></td>
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
<td><p>Write generated trips to FILE</p></td>
</tr>
<tr class="odd">
</tr>
</tbody>
</table>

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
<td><p>Sets the time of beginning of the simulation during the first day (in seconds); <em>default: <strong>0</strong></em></p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Sets the time of ending of the simulation during the last day (in seconds); <em>default: <strong>0</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Sets the duration of the simulation in days; <em>default: <strong>1</strong></em></p></td>
</tr>
<tr class="even">
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
<td><p>Detailed messages about every single step; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
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