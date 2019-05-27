---
title: Libsumo
permalink: /Libsumo/
---

The main way to interact with a running simulation is [TraCI](/TraCI "wikilink") which gives the complete flexibility of doing cross-platform, cross-language, and networked interaction with [SUMO](/SUMO "wikilink") acting as a server. One major drawback is the communication overhead due to the protocol and the socket communication. To have a more efficient coupling without the need to dive deep into the SUMO internals an interface called libsumo is being defined, having the following properties:

-   C++ interface based on static functions and a few simple wrapper classes for results
-   Function signatures similar to [TraCI](/TraCI "wikilink")
-   Language bindings for at least Java and Python
-   Based on [SWIG](http://www.swig.org/)

libsumo is still under development but several basic parts are already functional

-   loading a simulation
-   doing simulation steps
-   retrieving data from single vehicles, detectors, edges etc.

What does not work yet:

-   running with sumo-gui
-   subscriptions
-   vehicle state notifications (getting the number of departed vehicles etc.)
-   testing the whole stuff

Building it
-----------

It currently requires cmake and swig being installed together with the developer packages for Python (and Java if needed), for Windows see [Installing/Windows_CMake](/Installing/Windows_CMake "wikilink"). You need to (re-)compile sumo yourself under Windows following the remarks above, under Linux it is probably just a matter of calling cmake and make. For the python bindings you will get a libsumo.py and a _libsumo.so (or .pyd on Windows). If you place them somewhere on your python path you should be able to use them like that:

`import libsumo`
`libsumo.Simulation.load([`“`-c`”`, `“`test.sumocfg`”`])`
`libsumo.Simulation.simulationStep()`

Further descriptions will follow.