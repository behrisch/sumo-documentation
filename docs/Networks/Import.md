---
layout: post
title: Networks Import
permalink: /Networks/Import/
---

[NETCONVERT](/NETCONVERT "wikilink") allows to import road networks from different third-party formats. By now, the following formats are supported:

-   OpenStreetMap databases, see [Networks/Import/OpenStreetMap](/Networks/Import/OpenStreetMap "wikilink")
-   PTV VISUM (a macroscopic traffic simulation package), see [Networks/Import/VISUM](/Networks/Import/VISUM "wikilink")
-   PTV VISSIM (a microscopic traffic simulation package), see [Networks/Import/Vissim](/Networks/Import/Vissim "wikilink")
-   OpenDRIVE networks, see [Networks/Import/OpenDRIVE](/Networks/Import/OpenDRIVE "wikilink")
-   MATsim networks, see [Networks/Import/MATsim](/Networks/Import/MATsim "wikilink")
-   ArcView-data base files, see [Importing ArcView networks (shapefiles)](/Networks/Import/ArcView "wikilink")
-   Elmar Brockfelds unsplitted and splitted NavTeq-data, see [Networks/Import/DlrNavteq](/Networks/Import/DlrNavteq "wikilink")
-   RoboCup Rescue League folders, see [Networks/Import/RoboCup](/Networks/Import/RoboCup "wikilink")

In most of these cases, [NETCONVERT](/NETCONVERT "wikilink") needs only two parameter: the option named as the source application/format followed by the name of the file to convert and the name of the output file (using the option). In the case, a VISUM network shall be imported, the following code will convert it into a SUMO-network:

`netconvert --visum=MyVisumNet.inp --output-file=MySUMONet.net.xml`

The import can be influenced using [further NETCONVERT options](/Networks/Further_Options "wikilink").

The native format comes in the variant of [*plain-xml*](/Networks/Building_Networks_from_own_XML-descriptions#Node_Descriptions "wikilink") which is designed as a simple input format for [NETCONVERT](/NETCONVERT "wikilink") and in *.net.xml* which is the output format of [NETCONVERT](/NETCONVERT "wikilink") and which is enriched with heuristically derived data such as right-of-way rules and junction geometry. Both formats can be converted into each other without data loss.