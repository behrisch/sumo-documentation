---
title: TraCI Multi-Entry-Exit Detectors Value Retrieval
permalink: /TraCI/Multi-Entry-Exit_Detectors_Value_Retrieval/
---

Command 0xa1: Get MeMeDetector Variable
---------------------------------------

|          |                                    |
|:--------:|:----------------------------------:|
|   ubyte  |               string               |
| Variable | Multi-Entry/Multi-Exit Detector ID |

Asks for the value of a certain variable of the named [multi-entry/multi-exit (e3) detector](/Simulation/Output/Multi-Entry_Multi-Exit_Detectors_(E3) "wikilink"). The value returned is the state of the asked variable/value within the last simulation step. Please note that for asking values from your [multi-entry/multi-exit detectors](/Simulation/Output/Multi-Entry_Multi-Exit_Detectors_(E3) "wikilink") with TraCI, you have to define them in an additional input file (see [multi-entry/multi-exit (e3) detectors](/Simulation/Output/Multi-Entry_Multi-Exit_Detectors_(E3) "wikilink")) and cannot add them via TraCI (yet). The following variable values can be retrieved, the type of the return value is also shown in the table.

| Variable                                 | ValueType  | Description                                                                                                                                | [Python Method](/TraCI/Interfacing_TraCI_from_Python "wikilink")                                                                        |
|------------------------------------------|------------|--------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| id list (0x00)                           | stringList | Returns a list of ids of all multi-entry/multi-exit detectors within the scenario (the given DetectorID is ignored)                        | [getIDList](http://www.sumo.dlr.de/daily/pydoc/traci._multientryexit.html#MultiEntryExitDomain-getIDList)                               |
| count (0x01)                             | int        | Returns the number of multi-entry/multi-exit detectors within the scenario (the given DetectorID is ignored)                               | [getIDCount](http://www.sumo.dlr.de/daily/pydoc/traci._multientryexit.html#MultiEntryExitDomain-getIDCount)                             |
| last step vehicle number (0x10)          | int        | Returns the number of vehicles that have been within the named multi-entry/multi-exit detector within the last simulation step \[\#\];     | [getLastStepVehicleNumber](http://www.sumo.dlr.de/daily/pydoc/traci._multientryexit.html#MultiEntryExitDomain-getLastStepVehicleNumber) |
| last step mean speed (0x11)              | double     | Returns the mean speed of vehicles that have been within the named multi-entry/multi-exit detector within the last simulation step \[m/s\] | [getLastStepMeanSpeed](http://www.sumo.dlr.de/daily/pydoc/traci._multientryexit.html#MultiEntryExitDomain-getLastStepMeanSpeed)         |
| last step vehicle ids (0x12)             | stringList | Returns the list of ids of vehicles that have been within the named multi-entry/multi-exit detector in the last simulation step            | [getLastStepVehicleIDs](http://www.sumo.dlr.de/daily/pydoc/traci._multientryexit.html#MultiEntryExitDomain-getLastStepVehicleIDs)       |
| last step halting vehicles number (0x14) | int        | Returns the number of vehicles which were halting during the last time step                                                                | [getLastStepHaltingNumber](http://www.sumo.dlr.de/daily/pydoc/traci._multientryexit.html#MultiEntryExitDomain-getLastStepHaltingNumber) |
||

Response 0xb1: MeMeDetector Variable
------------------------------------

|          |                                    |                             |                  |
|:--------:|:----------------------------------:|:---------------------------:|:----------------:|
|   ubyte  |               string               |            ubyte            |   <return_type>  |
| Variable | Multi-Entry/Multi-Exit Detector ID | Return type of the variable | <VARIABLE_VALUE> |

The respond to a **“Command Get MeMeDetector Variable”**.

Notes
-----

-   You can find [some further description on multi-entry/multi-exit detectors](/Simulation/Output/Multi-Entry_Multi-Exit_Detectors_(E3) "wikilink")
