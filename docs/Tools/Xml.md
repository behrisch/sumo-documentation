---
title: Tools Xml
permalink: /Tools/Xml/
---

xml2csv.py
----------

This converts any of the sumo xml files into a flat csv (character separated values) representation. CSV-Files are easy to parse and can be opened in [LibreOffice](http://www.libreoffice.org/) or Microsoft Excel. Usage:

`python xml2csv.py input.xml`

With the option you can customize the field separator (default is **;**), the option defines a quoting character such as ' which will be used to quote all fields. Furthermore you can supply an xsd schema file using to aid the parsing and get headings also for attributes which may be not in the current file. If you give the additional option the input file will be validated against the schema. This requires [lxml](http://lxml.de/) to be installed.

Please note that instead of an input file name you can give a number which will be interpreted as a server port where the script listens for incoming connections and then reads the input data from. The name for the output file can be given using the option with the default being the path of the input file with the “.xml” suffix replaced by “.csv”.

The application is limited to simple hierarchies, where the root element may contain several different child elements but all of those are limited to only one type of child elements.

csv2xml.py
----------

This is the inverse tool to xml2csv.py. Usage:

`python csv2xml.py -x schema.xsd input.csv`

The options have the same meaning as above. For some file types as nodes, edges and routes the conversion is hard coded for all the others a [schema](/XMLValidation#Adding_a_schema_declaration "wikilink") must be provided. It is not possible to automatically perform validation on the output.

xml2protobuf.py
---------------

If the CSV representation is still too big you can compress the output even further using Google's [Protocol Buffers](https://developers.google.com/protocol-buffers/). This will require the protoc compiler as well as the protobuf packages for python and your target language to be installed. Usage:

`python xml2protobuf.py -x schema.xsd input.xml`

The xsd schema file needs to be given the using and the option will enable XML validation. The additional option will give a directory where the protobuf message definitions and the generated python module will be saved (default is the current working dir). The script will generate the protobuf description from the schema and then write a protomsg file containing the binary stream.

protobuf2xml.py
---------------

This is the inverse tool to xml2protobuf.py. Usage:

`python protobuf2xml.py -x schema.xsd input.protomsg`

The options have the same meaning as above.