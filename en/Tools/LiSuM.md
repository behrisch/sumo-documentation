---
layout: post
title: Tools LiSuM
permalink: /Tools/LiSuM/
---

[thumb|150px|right|LiSuM Logo](/File:LisaSumoIcon.png "wikilink")

LiSuM is a middleware that couples [LISA+](https://www.schlothauer.de/en/software-systems/lisa/) and SUMO helping to execute more complex traffic controls on the intersections than SUMO originally permits. SUMO communicates with the LISA+ virtual controller through LiSuM.

LISA+ is a proprietary software tool developed and commercialized by [Schlothauer & Wauer](https://www.schlothauer.de/) used to plan and evaluate complex intersections. The control logics created with it can be directly uploaded to real controllers or tested with SUMO (using LiSuM) and VISSIM, a proprietary microscopic 3D traffic simulator.

LiSuM was built on Java technology and thus can be run on any operating system. LiSuM is licensed under the [GPL](http://www.gnu.org/licenses/gpl.html) and its current version is the 1.0.0.

[thumb|550px|right|SUMO communicates with the LISA+ virtual controller through LiSuM](/File:flowws.png "wikilink")

Installation
------------

[thumb|350px|right|LiSuM Main window](/File:LISASumo.MainWindow.PNG "wikilink")

The installation of LiSuM is straightforward and it may not present major difficulties. It is recomended to have Java SE Runtime Environment (version 8 and later) and SUMO (version 0.29.0 and later) installed before beginning with the installation. In order to install it on a Windows machine just download and execute the provided *msi* file and follow its instructions. On Ubuntu or other Linux distributions download the provided *zip* file and unzip it in any directory of your choice; to start LiSuM, seek the *jar* file, open a terminal and execute it using the well-known <i>java -jar</i> command.

When LiSuM is started for the first time, the user is prompt to select a directory which is going to be used as the workspace directory. The workspace is the directory where LiSuM looks for existing simulation projects, where new ones should be stored and where the system preferences are saved. If needed use the system preferences window to change the workpace path.

Getting started
---------------

Open LiSuM, set the SUMO path in the system proferences dialog window and open an existing simulation project from the workspace. In the Tools menu, select “Start Lisa+ Virtual Controller” to start an instance of the LISA+ Virtual Controller. Pressing Ctrl+p or clicking on the “Play” button on the toolbar will open an instance of the SUMO-GUI, which will take control over the system. Almost all menus, toolbars and dialog windows of LiSuM get blocked and from hereon the simulation may be started, paused, resumed and stopped from SUMO. Only the Control Units Management dialog window stays enabled so it is possible to change the control units settings during the execution of the simulation.

For better understanding of how LiSuM works, you can play around with the two sample projects (sampleSimulation and simpleSampleSimulation) located in the workspace.

### Creating a new simulation project

A simulation project is a directory containing:

-   A LiSuM configuration file (lisum.xml)
-   SUMO files (\*.add.xml, \*.net.xml, \*.rou.xml, \*.sumocfg, etc)
-   A directory containing LISA+ control units files (exported from LISA+ to Vissim)

#### Configuration file

The LiSuM configuration file is a XML file (always named *lisum.xml*) which contains the necessary information to control the way LISA+ communicates with SUMO during the execution of a simulation by telling LiSuM how to match control units, signal groups and detectors to one another. The configuration file is basically composed of the mandatory elements `input` and `controlUnits` that is composed of the two non-mandatory tags `controlUnits` and `detectors`. Since LISA+ and SUMO use different naming conventions for their elements, the fields `controlUnits` and `detectors` tell LiSuM how are they called in each system.

[thumb|320px|right](/File:Classes.PNG "wikilink")

**Example:**

    <simulation>
       <input>
          <lisa>lisaDirectory</lisa>
       </input>

       <controlUnits>
          <controlUnit  lisa="z1_fg1" sumo="gneJ1" >
             <signalGroups>
                <signalGroup  lisa="K1" sumo="0" />
                <signalGroup  lisa="K2" sumo="1" />
                <signalGroup  lisa="K3" sumo="2" />
                <signalGroup  lisa="K4" sumo="3" />
             </signalGroups>

             <detectors>
                <detector  lisa="D1" sumo="myLoop1" />
             </detectors>
          </controlUnit>

          <controlUnit  lisa="z1_fg2" sumo="gneJ2" >
             <signalGroups>
                <signalGroup lisa="K1" sumo="0,1,2" />
                <signalGroup lisa="K2" sumo="3,4" />
                <signalGroup lisa="K3" sumo="5,6,7"/>
                <signalGroup lisa="K4" sumo="8" main="K3" />
             </signalGroups>
          </controlUnit>
       </controlUnits>
    </simulation>

[thumb|190px|right|Logging levels](/File:LoggingLevels.PNG "wikilink")

The configuration file shown above declares the following:

-   The LISA+ control unit files are in the directory <span style="background:#ffe6e6"><SIMULATION_DIRECTORY>/lisaDirectory</span>.
-   There are two control units where...
    -   the first control unit...
        -   matches the LISA+'s control unit <b><i>z1_fg1</i></b> with <b><i>gneJ1</i></b> in SUMO.
        -   is composed of four signal groups for LISA+ and four for SUMO
        -   contains one detector called D1 in LISA+ and myLoop1 in SUMO.
    -   and the second control unit...
        -   is called <b><i>z1_fg2</i></b> in LISA+ and <b><i>gneJ2</i></b> in SUMO.
        -   contains also four signal groups in LISA+ and 9 in SUMO, where, for example, the LISA+ signal group <b>K2</b> controls the behaviour of the SUMO signal groups number 3 and 4.
        -   the fourth signal group contains the attribute <span style="background:#ffe6e6">main</span> set to <b>K3</b>. This means that if the LISA+ signal group <b>K4</b> is disabled (<i>OFF</i>) at any time of the cycle, the SUMO signal group number 8 will take the state of the signal group <b>K3</b> of LISA+.

Tools
-----

### Control Units Management

[thumb|300px|right|Control units management window](/File:LISASumo.ControlUnitsOptionsWindow.PNG "wikilink")

The Control Units Managemente dialog window gets opened by pressing Ctrl+M or by clicking on the “Grid” button on the simulation toolbar. In this dialog it is possible to change the behaviour of all available control units of the simulation by turning them off and on, selecting the program, or enabling or disabling program settings like VA (Verkehrsabhänhig) and ÖV (Öffentliche Verkehrsmittel).

It is also possible to deactivate the communication with LISA+ by unclicking the check box right of the control units combo box (image below). Per default, LISA+ controls units not being assigned to any Sumo intersection appear disabled.

[thumb|170px|center|Checkbox to deactivate the communication with LISA+](/File:Controlunits_on.PNG "wikilink")

### LISA+ Virtual Controller

LISA+ provides an executable stand-alone Java JAR file containing an application called LISA+ Virtual Controller and is used to simulate control units devices and run control logics on it. Therefore it is not necessary to have LISA+ installed to be able to run LiSuM. This application is originally intended to be used with Vissim. The communication with LISA+ Virtual Controller happens over RESTful web services, the communication protocol is REST/HTTP and the data format is described using WSDL/XSD files, used to describe SOAP services.

It is necessary that, before starting SUMO, an instance of the LISA+ Virtual Controller is opened and running (clicking on *Menu: Tools -&gt; Start Lisa+ Virtual Controller* or by pressing Ctrl+r).

Per default the LISA+ Virtual Controller and its configuration file (OmlFgServer.ini) are to be found in the <span style="background:#ffe6e6">OmlFgServer</span> directory located in the LiSuM installation directory. This path can be changed in the System Preferences Window (*Menu: Tools -&gt; Preferences*).

[thumb|400px|right|LISA+ Virtual Controller (Windows 7)](/File:VirtualController.PNG "wikilink")

### Simulations directory

Per default, LiSuM searches for simulations in the <span style="background:#ffe6e6">simulations</span> directory, which can be found in the instalation directory (.../DLR/LiSuM/). The simulations directory can be changed in the <i>System Preferences Window</i> (*Menu: Tools -&gt; System Preferences*).

Miscellaneous
-------------

### The green phase matching problem

While LISA+ only defines and uses only one green phase, SUMO uses two different types of them: <b><i>g</i></b> (no priority) and <b><i>G</i></b> (priority). This way, when LISA+ switches a signal group to green, LiSuM has to decide which of the two types of green may send to the corresponding SUMO signal group. Since there is no ideal solution to this problem so a heuristic approach is applied: LiSuM decides in forehand which green phase each SUMO signal group will ALWAYS receive based on the number of <b><i>G</i></b><i>s</i> and <b><i>g</i></b><i>s</i> that each signal group has in their configuration strings in the net.xml file of the simulations project (tag tlLogic), having <b><i>G</i></b> priority over <b><i>g</i></b>.

Some examples:

-   <phase duration="31" state="GGggrrrrGGggrrrr"/>` → This signal group will always switch to `<b><i>`G`</i></b>
-   <phase duration="5"  state="yyggrrrryyggrrrr"/>` → This signal group will always switch to `<b><i>`g`</i></b>
-   <phase duration="6"  state="rrGGrrrrrrGGrrrr"/>` → This signal group will always switch to `<b><i>`G`</i></b>
-   <phase duration="5"  state="rryyrrrrrryyrrrr"/>` → This signal group will always switch to `<b><i>`G`</i></b>
-   <phase duration="31" state="rrrrGGggrrrrGggg"/>` → This signal group will always switch to `<b><i>`g`</i></b>
