---
title: XMLValidation
permalink: /XMLValidation/
---

__TOC__

Validation of XML inputs
========================

All [SUMO applications](/Sumo_at_a_Glance#Included_Applications "wikilink") support XML validation for their inputs. To enable this, the following options can be used:

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
<td><p>Set schema validation scheme of XML inputs (“never”, “auto” or “always”); <em>default: <strong>auto</strong></em></p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Set schema validation scheme of SUMO network inputs (“never”, “auto” or “always”); <em>default: <strong>never</strong></em></p></td>
</tr>
<tr class="odd">
</tr>
</tbody>
</table>

Validation is performed by activating [XML schema processing](https://xerces.apache.org/xerces-c/schema-3.html) in the XML parser. This catches many common input errors such as spelling mistakes and attributes which should have been placed within another element.

Another prerequisite for validation is a schema deceleration within the root element of the input file such as

    <routes xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://sumo.dlr.de/xsd/routes_file.xsd">

When setting the validation options to *always* it is an error to omit this declaration.

Schema validation may slowdown XML parsing considerably and is therefore disabled for the network input by default (because networks should not be edited by hand and therefore be valid anyway).

.

Adding a schema declaration
===========================

Files that are written by one of the SUMO applications automatically receive the appropriate schema declaration. When writing an input file from scratch the schema declaration must be added manually to the root element as follows:

    <ROOT_ELEMENT xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="http://sumo.dlr.de/xsd/SCHEMA_FILE">

where *ROOT_ELEMENT* and *SCHEMA_FILE* should be set according to the following table:

| Application Option | ROOT_ELEMENT | SCHEMA_FILE          |
|--------------------|---------------|-----------------------|
| }, , ,             | routes        | routes_file.xsd      |
|                    | add           | additional_file.xsd  |
|                    | nodes         | nodes_file.xsd       |
|                    | edges         | edges_file.xsd       |
|                    | connections   | connections_file.xsd |
|                    | tlLogics      | tllogic_file.xsd     |
|                    | types         | types_file.xsd       |
|                    | meandata      | meandata_file.xsd    |
||

Schema Files
============

The schema files can be found in the /data/xsd directory of your SUMO installation. If the [environment variable *SUMO_HOME* is set](/Basics/Basic_Computer_Skills#Additional_Environment_Variables "wikilink"), these files will be used when validation inputs.

Otherwise, the files are loaded from *<http://sumo.dlr.de/xsd/SCHEMA_FILE>* which may slow down the application (or fail if there is no internet connection).

SUMO File Types
===============

A complete listing of file extensions used by [SUMO Applications](/Sumo_at_a_Glance#Included_Applications "wikilink") is given at [File_Extensions](/Other/File_Extensions "wikilink").