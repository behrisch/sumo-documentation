---
title: Basics Notation
permalink: /Basics/Notation/
---

The documentation within this wiki uses coloring to differ between different type of information. Below, these annotations and colors are described.

Command Line
------------

If you encounter something like this:

`netconvert --visum=MyVisumNet.inp --output-file=MySUMONet.net.xml`

you should know that this is a call on the command line. There may be also a '\\' at the end of a line. This indicates that you have to continue typing without pressing return (ignoring both the '\\' and the following newline). The following example means exactly the same as the one above:

`netconvert --visum=MyVisumNet.inp \`
`  --output-file=MySUMONet.net.xml`

Application Options
-------------------

Command line option names are normally coloured . Their values .

XML Examples
------------

XML-elements and attributes are shown <span class="inlxml">like this</span>. Their values, if variable, <span class="inlxml">*<LIKE THIS>*</span>.

Complete examples of XML-Files are shown like the following:

    <myType>
       <myElem myAttr1="0" myAttr2="0.0"/>
       <myElem myAttr1="1" myAttr2="-500.0"/>
    </myType>

Referenced Data Types
---------------------

-   *<BOOL>*: a boolean value, use “t” or “true” and “f” or “false” for encoding
-   *<INT>*: an integer value, may be negative
-   *<UINT>*: an unsigned integer value, must be &gt;=0
-   *<FLOAT>*: a floating point number
-   *<TIME>*: time, given in seconds; fractions are allowed, e.g. “12.1”
-   *<STRING>*: any string, but use ASCII-characters only
-   *<ID>*: a string which must not contain the following characters: '\#'

-   *<FILE>* or *<FILENAME>*: the (relative or absolute) path to a file; see also [\#Referenced File Types](/#Referenced_File_Types "wikilink")
-   *<PATH>*: a (a relative or absolute) path (usually to a folder)
-   *<COLOR>*: a quadruple of floats separated by ',' (*<FLOAT>*,*<FLOAT>*,*<FLOAT>*,*<FLOAT>*), which describe the red, green, blue, and alpha component ranging from 0.0 to 1.0 (the alpha component is optional), alternatively the list may contain integers in the 0-255 range. Please note that the separator must be a comma and there are no spaces allowed. The color may also be defined using a single string with a [HTML color code](http://en.wikipedia.org/wiki/Web_colors#Hex_triplet) or one of the basic colors (“red”, “green”, “blue”, “yellow”, “cyan”, “magenta”, “black”, “white”, “grey”)
-   *&lt;2D-POSITION&gt;*: two floats separated by ',' (*<FLOAT>*,*<FLOAT>*), which describe the x- and the y-offset, respectively. z is 0 implicitly
-   *&lt;3D-POSITION&gt;*: three floats separated by ',' (*<FLOAT>*,*<FLOAT>*,*<FLOAT>*), which describe the x- , y- and the z-offset, respectively
-   *<POSITION-VECTOR>*: A list of 2D- or 3D-Positions separate by ' '. I.e. (*&lt;2D-POSITION&gt;* *&lt;2D-POSITION&gt;*,*&lt;3D-POSITION&gt;*)
-   *&lt;2D-BOUNDING_BOX&gt;*: four floats separated by ',' (*<FLOAT>*,*<FLOAT>*,*<FLOAT>*,*<FLOAT>*), which describe x-minimum, y-minimum, x-maximum, and y-maximum
-   *<PROJ_DEFINITION>*: a string containing the projection definition as used by proj.4; please note that you have to embed the definition string in quotes

### Referenced File Types

-   *<NETWORK_FILE>*: a [SUMO network file](/Networks/SUMO_Road_Networks "wikilink") as built by [NETGENERATE](/NETGENERATE "wikilink") or [NETCONVERT](/NETCONVERT "wikilink")
-   *<ROUTES_FILE>*: a [SUMO routes file](/Definition_of_Vehicles,_Vehicle_Types,_and_Routes "wikilink") as built by [DUAROUTER](/DUAROUTER "wikilink") or [JTRROUTER](/JTRROUTER "wikilink") or by hand
-   *<TYPE_FILE>*: a [SUMO edge type file](/SUMO_edge_type_file "wikilink"), built by hand or downloaded
-   *<OSM_FILE>*: a [OpenStreetMap file](/OpenStreetMap_file "wikilink") as exported from [OpenStreetMap](http://www.openstreetmap.org/)

Further Schemes
---------------

Brackets '\[' and '\]' indicate that the enclosed information is optional. Brackets '&lt;' and '&gt;' indicate a variable - insert your own value in here.

is the path you have saved your SUMO-package into.