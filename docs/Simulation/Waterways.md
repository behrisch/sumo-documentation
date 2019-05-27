---
layout: post
title: Simulation Waterways
permalink: /Simulation/Waterways/
---

Waterway Simulation
===================

This page describes simulations of (inland) waterways in SUMO.

Approaches to ship modelling
============================

Currently, no exclusive movement model for ships is implemented. Instead the existing models for vehicle movement need to be re-purposed. By setting , vehicles are drawn in a more appropriate shape.

Problems and workarounds
------------------------

-   Due to the one-way nature of edges in sumo, ships cannot overtake each other by using the whole width of the waterway. To allow overtaking, multiple lanes have to be defined.
-   Since the right-of-way rules for ships are more complex than those for road vehicles, waterway intersections are set to by default.

Building a network for waterway simulation
==========================================

Waterways can be imported from [OSM](/Networks/Import/OpenStreetMap "wikilink") by adding the type map [osmNetconvertShips.typ.xml](http://sumo.dlr.de/trac.wsgi/browser/trunk/sumo/data/typemap/osmNetconvertShips.typ.xml). They can also be explicitly specified by setting .