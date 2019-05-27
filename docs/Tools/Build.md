---
layout: post
title: Tools Build
permalink: /Tools/Build/
---

Build Tools
===========

Code Cleaning Tools
===================

apply_astyle.py
----------------

Applies [astyle](http://astyle.sourceforge.net/) with pre-defined settings to all .cpp and .h files in the src tree. The position of the tree is determined relative to the position of the script. This call is usually done directly before releasing.

Call:

`apply_astyle.py`

Documentation Tools
===================

buildHTMLDocs.py
----------------

Converts wiki-documentation into static HTML pages. It removes the wiki navigation and adds user doc navigation while keeping the contents intact. This script is called by the main Makefile if “make docs” is called. If the script is called with an argument, it tries to fetch the wiki site with the given name, if not it retrieves all sites listed in the [table of contents](/SUMO_User_Documentation "wikilink"). Call “buildHTMLDocs.py --help” for a complete list of options.

Call:

`buildHTMLDocs.py SUMO`

checkAuthors.py
---------------

Checks the log for all source files for authors and “thanks” and checks whether they appear in the file header. It can optionally try to fix the file header and also update the global AUTHORS file if needed.

Call:

`checkAuthors.py`