---
title: Simulation Railways
permalink: /Simulation/Railways/
---

Train Simulation
================

This page describes simulations of trains in SUMO. To build an intermodal simulation scenario with trains, additional steps have to be take in comparison to a plain vehicular simulation.

Approaches to train modelling
=============================

Currently, no exclusive movement model for trains is implemented. Instead the existing models for vehicle movement need to be re-purposed.

Building a network for train simulation
=======================================

Railways
--------

Railways can be imported from [OSM](/Networks/Import/OpenStreetMap "wikilink"). They can also be explicitly specified using the existing *vClasses*.

Bidirectional track usage
-------------------------

Bidirectional track usage is modelled by two edges that have their geometries exactly reversed and using the attribute . This will result in lane geometries that are overlayed exactly. These edges are referred to as *superposed* (alternatively as bidirecticional rail edges).

Rail signals recognize superposed edges and automatically restrict their usage so that only one direction is accessible at a time.

When importing networks from [OSM](/Networks/Import/OpenStreetMap "wikilink"), rails tagged with are automatically imported as superposed edges.

[SUMO-GUI](/SUMO-GUI "wikilink") automatically shows only one of both edges to avoid duplicate drawing of cross-ties. The visualisation option *show lane direction* can be used to identifiy superposed edges as arrows in both directions will be show.

[NETEDIT](/NETEDIT "wikilink") supports the visualisation option *spread superposed* which draws both edges with an offset and thus makes it easier to edit them.

Rail Signals
------------

The [node type](/Networks/Building_Networks_from_own_XML-descriptions#Node_Descriptions "wikilink") may be used to define signals which implement [Automatic Block Signaling](http://en.wikipedia.org/wiki/Automatic_block_signaling).

Rail Crossings
--------------

The [node type](/Networks/Building_Networks_from_own_XML-descriptions#Node_Descriptions "wikilink") may be used to define railway crossings. At these nodes trains will always have the right of way and road vehicles get a red light until there is a safe gap between approaching trains.

When importing networks from [OpenStreetMap](/Networks/Import/OpenStreetMap "wikilink"), rail crossings will be imported automatically. For other input data sources the crossings may have to be specified [via additional xml files](/Tutorials/ScenarioGuide#Modifying_an_imported_network_via_plain.xml "wikilink") or set via [NETEDIT](/NETEDIT "wikilink") after importing.