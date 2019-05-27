---
title: DFROUTER
permalink: /DFROUTER/
---

From 30.000 feet
================

**DFROUTER** uses induction loop values to compute vehicle routes that may be used by [SUMO](/SUMO "wikilink").


**Purpose:** Building vehicle routes from induction loop counts

**System:** portable (Linux/Windows is tested); runs on command line

**Input (mandatory):**
A) a road network as generated via [NETCONVERT](/NETCONVERT "wikilink") or [NETGENERATE](/NETGENERATE "wikilink"), see [Building Networks](/SUMO_User_Documentation#Network_Building "wikilink")

B) induction loop definitions

C) induction loop measures

**Output:** [Definition of Vehicles, Vehicle Types, and Routes](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes "wikilink") usable by [SUMO](/SUMO "wikilink")

**Programming Language:** C++

Usage Description
=================

A high level description can be found at [Demand/Routes_from_Observation_Points](/Demand/Routes_from_Observation_Points "wikilink"). The complete list of options is given in the following.

Options
-------

You may use a XML schema definition file for setting up a DFROUTER configuration: [dfrouterConfiguration.xsd](http://sumo.dlr.de/xsd/dfrouterConfiguration.xsd).

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
<td><p>Loads the SUMO-network FILE</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Loads detector descriptions from FILE</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Loads detector flows from FILE(s)</p></td>
</tr>
<tr class="even">
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
<td><p>Saves computed routes to FILE</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Forces DFROUTER to compute routes for in-between detectors; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Saves typed detectors to FILE</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Saves detector positions as pois to FILE</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Saves emitter definitions for source detectors to FILE</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Add vehicle types to the emitters file (PKW, LKW); <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Write generated vehicle types into separate FILE instead of including them into the emitters-output</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Saves emitter positions as pois to FILE</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Saves variable seed sign definitions for sink detectors to FILE</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Saves rerouter definitions for sink detectors to FILE</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><dl>
<dt><em>default: <strong>false</strong></em></dt>

</dl></td>
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
<td><p>Derive missing flow values from upstream or downstream (not working!); <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Switches to highway-mode; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Only warn about unparseable detectors; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Recomputes detector types even if given; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Recomputes routes even if given; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Keeps routes even if they have exhausted max-search-depth; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Keeps routes even if a shorter one exists; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Number of edges to follow a route without passing a detector; <em>default: <strong>30</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Writes only emission times; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Do not route on these edges</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Allow turnarounds as route continuations; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Minimum distance in meters between start and end node of every route; <em>default: <strong>-1</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>generate random departure times for emitted vehicles; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Multiply flow times with TIME to get seconds; <em>default: <strong>60</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Subtracts TIME seconds from (scaled) flow times; <em>default: <strong>0</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Expected distance between two successive data sets; <em>default: <strong>60</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Write calibrators to FILE; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><dl>
<dt><em>default: <strong>false</strong></em></dt>

</dl></td>
</tr>
<tr class="odd">
<td></td>
<td><dl>
<dt><em>default: <strong>false</strong></em></dt>

</dl></td>
</tr>
<tr class="even">
<td></td>
<td><p>Removes empty detectors from the list; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><dl>
<dt><em>default: <strong>false</strong></em></dt>

</dl></td>
</tr>
<tr class="even">
<td></td>
<td><p>Try to determine further inflows to an inbetween detector when computing split probabilities; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Scale factor for flows; <em>default: <strong>1</strong></em></p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

### Defaults

| Option | Description                                                 |
|--------|-------------------------------------------------------------|
|        | Assigns a default depart lane                               |
|        | Assigns a default depart position                           |
|        | Assigns a default depart speed                              |
|        | Assigns a default arrival lane                              |
|        | Assigns a default arrival position                          |
|        | Assigns a default arrival speed                             |
|        | The default speed deviation of vehicles; *default: **0.1*** |
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
<td><p>Defines the begin time; Previous defs will be discarded; <em>default: <strong>0</strong></em></p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Defines the end time; Later defs will be discarded; Defaults to one day; <em>default: <strong>86400</strong></em></p></td>
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
<td><p>Lists detectors with no flow (enable -v); <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Prints aggregated detector flows; <em>default: <strong>false</strong></em></p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Disable console output of route parsing step; <em>default: <strong>false</strong></em></p></td>
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