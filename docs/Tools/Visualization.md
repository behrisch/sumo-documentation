---
title: Tools Visualization
permalink: /Tools/Visualization/
---

[SUMO](/SUMO "wikilink") offers a wide range of [outputs](/Simulation/Output "wikilink"), but one may find it hard to parse and visualize them. Below, you may find some tools that allow to visualize a simulation run's results for being included in a scientific paper. Additional tools read plain .csv-files and were added to the suite as they offer a similar interface.

All these tools are just wrappers around the wonderful [matplotlib](http://matplotlib.org/) library. If you are familiar with Python, you must have a look.

The tools share a set of [common options](/#common_options "wikilink") to fine-tune the appearence of the generated figures. These options' names where chosen similar to the [matplotlib](http://matplotlib.org/) calls.

The tools are implemented in Python and need [matplotlib](http://matplotlib.org/) to be installed. The tools can be found in /tools/visualization.

Current Tools
=============

Below, you will find the descriptions of tools that should work with the current outputs [SUMO](/SUMO "wikilink")/[SUMO-GUI](/SUMO-GUI "wikilink") generate. To run them, you'll need:

-   to install Python
-   to install [matplotlib](http://matplotlib.org/)
-   to set

All scripts are executed from the command line and you have to give the command line options as listed in the descriptions below. Please note that [\#common options](/#common_options "wikilink") may be applied to all the scripts listed in the following sub-sections albeit few options may not work for certain scripts.

plot_net_dump.py
------------------

plot_net_dump.py shows a network, where the network edges' colors and width are set in dependence to defined edge attributes. The edge weights are read from “edgedumps” - [edgelane traffic](/Simulation/Output/Lane-_or_Edge-based_Traffic_Measures "wikilink"), [edgelane emissions](/Simulation/Output/Lane-_or_Edge-based_Emissions_Measures "wikilink"), or [edgelane noise](/Simulation/Output/Lane-_or_Edge-based_Noise_Measures "wikilink").

<table>
<tbody>
<tr class="odd">
<td><p><a href="/Image:plot_net_dump.png" title="wikilink">300px</a></p></td>
<td><p><code>python plot_dump_net.py -v -n bs.net.xml \</code><br />
<code> --xticks 7000,14001,2000,16 --yticks 9000,16001,1000,16 \</code><br />
<code> --measures entered,entered --xlabel [m] --ylabel [m] \</code><br />
<code> --default-width 1 -i base-jr.xml,base-jr.xml \</code><br />
<code> --xlim 7000,14000 --ylim 9000,16000 -\</code><br />
<code> --default-width .5 --default-color #606060 \</code><br />
<code> --min-color-value -1000 --max-color-value 1000 \</code><br />
<code> --max-width-value 1000 --min-width-value -1000  \</code><br />
<code> --max-width 3 --min-width .5 \</code><br />
<code> --colormap #0:#0000c0,.25:#404080,.5:#808080,.75:#804040,1:#c00000</code></p>
<p>It shows the shift in traffic in the city of Brunswick, Tuesday-Thursday week type after establishing an environmental zone.</p></td>
</tr>
<tr class="even">
<td><p><a href="/Image:plot_net_dump2.png" title="wikilink">300px</a></p></td>
<td><p><code>python plot_dump_net.py -v -n bs.net.xml \</code><br />
<code> --xticks 7000,14001,2000,16 --yticks 9000,16001,1000,16 \</code><br />
<code> --measures NOx_normed,NOx_normed --xlabel [m] --ylabel [m] \</code><br />
<code> --default-width 1 -i HBEFA_base-jr.xml,HBEFA_base-jr.xml \</code><br />
<code> --xlim 7000,14000 --ylim 9000,16000 \</code><br />
<code> --default-width .5 --default-color #606060 \</code><br />
<code> --min-color-value -.1 --max-color-value .1 \</code><br />
<code> --max-width-value .1  --max-width 3 --min-width .5 \</code><br />
<code> --colormap #0:#00c000,.25:#408040,.5:#808080,.75:#804040,1:#c00000</code></p>
<p>Showing the according changes in NOx emissions.</p></td>
</tr>
<tr class="odd">
</tr>
</tbody>
</table>

Look, all these scripts have capabilities for being improved, this one especially.

-   both, as well as expect two entries being divided by a ','. The first is used for the edges' color, the second for their widths. But you may simply skip one entry. Then, the deafult values are used.
-   dump-files cover usually more than one interval, but the script stops after the first one (only the first one is plotted)

**Options**

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
<td><p>Defines the network to read</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Defines the dump-output files to use as input</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Define which measure to plot;default: speed,entered</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Defines the default edge width; default: .1</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>If set, the progress is printed on the screen</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Defines the minimum edge width; default: .5</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Defines the maximumedge width; default: 3</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>If set, colors are log-scaled</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>If set, widths are log-scaled</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>If set, defines the minimum edge color value</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>If set, defines the maximum edge color value</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>If set, defines the minimum edge width value</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>If set, defines the maximum edge width value</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>If set, the progress is printed on the screen</p></td>
</tr>
<tr class="odd">
</tr>
</tbody>
</table>

plot_net_selection.py
-----------------------

plot_net_selection.py reads a road network and a selection file as written by [SUMO-GUI](/SUMO-GUI "wikilink"). It plots the road network, choosing a different color and width for the edges which are within the selection (all edge with at least one lane in the selection).

<table>
<tbody>
<tr class="odd">
<td><p><a href="/Image:plot_net_selection.png" title="wikilink">300px</a></p></td>
<td><p><code>python plot_selection.py -n bs.net.xml \</code><br />
<code> --xlim 7000,14000 --ylim 9000,16000 \</code><br />
<code> -i selection_environmental_zone.txt \</code><br />
<code> --xlabel [m] --ylabel [m] \</code><br />
<code> --xticks 7000,14001,2000,16 --yticks 9000,16001,1000,16 \</code><br />
<code> --selected-width 1 --edge-width .5 -o selected_ez.png \</code><br />
<code> --edge-color #606060 --selected-color #800000 </code></p>
<p>The example shows the selection of an “environmental zone”.</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

**Options**

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
<td><p>Defines the network to read</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Defines selection file to read</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Defines the width for selected edges;default: 1</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Defines the color for selected edges; default: r (red)</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Defines the default edge width; default: .2</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Defines the default edge color; default: #606060</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>If set, the progress is printed on the screen</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

plot_net_speeds.py
--------------------

plot_net_speeds.py reads a road network and plots it using the allowed speeds to color the edges. It is rather an example for using measures read from the network file.

<table>
<tbody>
<tr class="odd">
<td><p><a href="/Image:plot_net_speeds.png" title="wikilink">300px</a></p></td>
<td><p><code>python plot_speeds.py -n bs.net.xml --xlim 1000,25000 \</code><br />
<code> --ylim 2000,26000 --edge-width .5 -o speeds2.png \</code><br />
<code> --minV 0 --maxV 60 --xticks 16 --yticks 16 \</code><br />
<code> --xlabel [m] --ylabel [m] --xlabelsize 16 --ylabelsize 16 \</code><br />
<code> --colormap jet</code></p>
<p>The example colors the streets in Brunswick, Germany by their maximum allowed speed.</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

**Options**

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
<td><p>Defines the network to read</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Defines the default edge width; default: .2</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Defines the default edge color; default: #606060</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Define the minimum value boundary</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Define the maximum value boundary</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>If set, the script says what it's doing</p></td>
</tr>
<tr class="odd">
</tr>
</tbody>
</table>

plot_net_trafficLights.py
---------------------------

plot_net_trafficLights.py reads a road network and plots it and additionally adds dots/markers at the position of traffic lights that are part of the net.

<table>
<tbody>
<tr class="odd">
<td><p><a href="/Image:plot_net_trafficLights.png" title="wikilink">300px</a></p></td>
<td><p><code>python plot_trafficLights.py -n bs.net.xml \</code><br />
<code> --xlim 1000,25000 --ylim 2000,26000 --edge-width .5 \</code><br />
<code> --xticks 16 --yticks 16 --xlabel [m] --ylabel [m] \ </code><br />
<code> --xlabelsize 16 --ylabelsize 16 --width 5 \</code><br />
<code> --edge-color #606060</code></p>
<p>The example shows the traffic lights in Brunswick.</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

**Options**

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
<td><p>Defines the network to read</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Defines the default edge width; default: .2</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Defines the default edge color; default: #606060</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Define the minimum value boundary</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Define the maximum value boundary</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>If set, the script says what it's doing</p></td>
</tr>
<tr class="odd">
</tr>
</tbody>
</table>

plot_summary.py
----------------

plot_summary.py reads one or multiple [summary-files](/Simulation/Output/Summary "wikilink") and plots a selected measure (attribute of the read [summary-files](/Simulation/Output/Summary "wikilink")). The measure is visualised as a time line along the simulation time.

<table>
<tbody>
<tr class="odd">
<td><p><a href="/Image:summary_running.png" title="wikilink">300px</a></p></td>
<td><p><code>python plot_summary.py </code><br />
<code> -i mo.xml,dido.xml,fr.xml,sa.xml,so.xml \</code><br />
<code> -l Mo,Di-Do,Fr,Sa,So --xlim 0,86400 --ylim 0,10000 </code><br />
<code> -o sumodocs/summary_running.png --yticks 0,10001,2000,14 \</code><br />
<code> --xticks 0,86401,14400,14 --xtime1 --ygrid \</code><br />
<code> --ylabel </code>“<code>running</code><code> </code><code>vehicles</code><code> </code><code>[#]</code>”<code> --xlabel </code>“<code>time</code>”<code> \</code><br />
<code> --title </code>“<code>running</code><code> </code><code>vehicles</code><code> </code><code>over</code><code> </code><code>time</code>”<code> --adjust .14,.1 </code></p>
<p>The example shows the numbers of vehicles running in a large-scale scenario of the city of Brunswick over the day for the standard week day classes. “mo.xml”, “dido.xml”, “fr.xml”, “sa.xml”, and “so.xml” are <a href="/Simulation/Output/Summary" title="wikilink">summary-files</a> resulting from simulations of the weekday-types Monday, Tuesday-Thursday, Friday, Saturday, and Sunday, respectively.</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

**Options**

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
<td><p>Defines the <a href="/Simulation/Output/Summary" title="wikilink">summary-file</a>(s) to read</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Defines the measure to read from the summary file; default: <em>running</em></p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>If set, the progress is printed on the screen</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

plot_tripinfo_distributions.py
--------------------------------

plot_tripinfo_distributions.py reads one or multiple [tripinfo-files](/Simulation/Output/TripInfo "wikilink") and plots a selected measure (attribute of the read [tripinfo-files](/Simulation/Output/TripInfo "wikilink")). The measure is visualised as vertical bars that represent the numbers of occurences of the measure (vehicles) that fall into a bin.

<table>
<tbody>
<tr class="odd">
<td><p><a href="/Image:tripinfo_distribution_duration.png" title="wikilink">300px</a></p></td>
<td><p><code>python plot_tripinfo_distributions.py \</code><br />
<code> -i mo.xml,dido.xml,fr.xml,sa.xml,so.xml \</code><br />
<code> -o tripinfo_distribution_duration.png -v -m duration \</code><br />
<code> --minV 0 --maxV 3600 --bins 10 --xticks 0,3601,360,14 \</code><br />
<code> --xlabel </code>“<code>duration</code><code> </code><code>[s]</code>”<code> --ylabel </code>“<code>number</code><code> </code><code>[#]</code>”<code> \</code><br />
<code> --title </code>“<code>duration</code><code> </code><code>distribution</code>”<code> \</code><br />
<code> --yticks 14 --xlabelsize 14 --ylabelsize 14 --titlesize 16 \</code><br />
<code> -l mon,tue-thu,fri,sat,sun --adjust .14,.1 --xlim 0,3600</code></p>
<p>The example shows the travel time distribution for the vehicles of different week day classes (Braunschweig scenario). “mo.xml”, “dido.xml”, “fr.xml”, “sa.xml”, and “so.xml” are <a href="/Simulation/Output/TripInfo" title="wikilink">tripinfo-files</a> resulting from simulations of the weekday-types Monday, Tuesday-Thursday, Friday, Saturday, and Sunday, respectively.</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

**Options**

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
<td><p>Defines the <a href="/Simulation/Output/Summary" title="wikilink">summary-file</a>(s) to read</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Defines the measure to read from the summary file</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>If set, the progress is printed on the screen</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>The number of bins to devide the values into</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Defines a number by which read values are divided; default: 1.0</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>The minimum value; if set, read values that are lower than this value are set to this value</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>The maximum value; if set, read values that are higher than this value are set to this value</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

plot_csv_timeline.py
----------------------

plot_csv_timeline.py reads a .csv file and plots columns selected using the option. The values are visualised as lines.

<table>
<tbody>
<tr class="odd">
<td><p><a href="/Image:nefz.png" title="wikilink">300px</a></p></td>
<td><p><code>plot_csv_timeline.py \</code><br />
<code> -i nefz.csv -c 1 --no-legend --xlabel </code>“<code>time</code><code> </code><code>[s]</code>”<code> \</code><br />
<code> --ylabel </code>“<code>velocity</code><code> </code><code>[km/h]</code>”<code> --xlabelsize 14 --ylabelsize 14 \</code><br />
<code> --xticks 14 --yticks 14 --colors k --ylim 0,125 \</code><br />
<code> --output nefz.png \</code><br />
<code> --title </code>“<code>New</code><code> </code><code>European</code><code> </code><code>Driving</code><code> </code><code>Cycle</code><code> </code><code>(NEDC)</code>”<code> --titlesize 16</code></p>
<p>The example shows the <a href="/Tools/Emissions#Driving_Cycles" title="wikilink">New European Driving Cycle (NEDC)</a>.</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

**Options**

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
<td><p>Defines the input file to use</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Defines which columns shall be plotted</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>If set, the progress is printed on the screen</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

plot_csv_pie.py
-----------------

plot_csv_pie.py reads a .csv file that is assumed to contain a name in the first and an according value in the second column. The read name/value-pairs are visualised as a pie chart.

<table>
<tbody>
<tr class="odd">
<td><p><a href="/Image:paradigm.png" title="wikilink">300px</a></p></td>
<td><p><code>plot_csv_pie.py \</code><br />
<code> -i paradigm.csv -b --colormap Accent --no-legend -s 6,6 </code></p>
</td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

**Options**

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
<td><p>Defines the input file to read</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Interprets read measures as percentages</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Reverts the order of read values before plotting them</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Does not plot the labels</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Puts a shadow below the circle</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Sets the start angle</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>If set, the progress is printed on the screen</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

plot_csv_bars.py
------------------

plot_csv_bars.py reads a .csv file that is assumed to contain a name in the first and an according value in the second column. The read name/value-pairs are visualised as a bar chart.

<table>
<tbody>
<tr class="odd">
<td><p><a href="/Image:nox_effects_bars.png" title="wikilink">300px</a></p></td>
<td><p><code>plot_csv_bars.py \</code><br />
<code> -i nox_effects.txt --colormap RdYlGn --no-legend --width .4 \</code><br />
<code> -s 8,4 --revert --xlim 0,50 --xticks 0,51,10,16 --yticks 16 \</code><br />
<code> --adjust .28,.1,.95,.9 --show-values </code></p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

**Options**

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
<td><p>Defines the csv file to use as input</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Defines which column of the read .csv-file shall be plotted; default: 1</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Reverts the order of read values before plotting them</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Defines the width of the bars; default: .8</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Defines the space between the bars; default: .2</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Defines a number by which read values are divided; default: 1.0</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Shows the values</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Position offset for values</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Draws vertical bars (default are horizontal bars)</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Does not plot the labels</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>If set, the progress is printed on the screen</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

common options
--------------

The following options are common to all previously listed tools. They can be divided into two groups:

-   options for formatting the figure (including adding captions etc.)
-   options for determining what to do with the generated figure

The options are listed and discussed in the following sub-sections, respectively.

### Formatting Options

<table>
<thead>
<tr class="header">
<th><p>Option</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td></td>
<td><p>Uses the given colors; the number of given colors must be the same as the number of measures to plot</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Uses the named colormap</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>Uses the given labels; the number of given labels must be the same as the number of measures to plot</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Describes the limits of the figure along the x-axis</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Describes the limits of the figure along the y-axis</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>If only one number is given, it is interpreted as the size of the tick labels on the x-axis; if four numbers are given, they are interpreted as the lowest ticks position, the highest ticks position, the step between ticks, and the tick's size, respectively, all along the x-axis</p></td>
</tr>
<tr class="odd">
<td>
<p><br />
</p></td>
<td><p>If only one number is given, it is interpreted as the size of the tick labels on the y-axis; if four numbers are given, they are interpreted as the lowest ticks position, the highest ticks position, the step between ticks, and the tick's size, respectively, all along the y-axis</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>If set, the tick labels along the x-axis are formatted as time entries (hh:mm)</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>If set, the tick labels along the y-axis are formatted as time entries (hh:mm)</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>If set, the tick labels along the x-axis are formatted as time entries (hh:mm:ss)</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>If set, the tick labels along the y-axis are formatted as time entries (hh:mm:ss)</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>If set, a grid along the ticks on the x-axis is drawn</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>If set, a grid along the ticks on the y-axis is drawn</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>The orientation of the x-ticks (in °); default: matplotlib default</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>The orientation of the y-ticks (in °); default: matplotlib default</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Defines the label to set for the x-axis</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Defines the label to set for the y-axis</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Defines the size of the label of the x-axis</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Defines the size of the label of the y-axis</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>Defines the title of the figure</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Defines the size of the title</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>Adjust the plot; If two floats are given, they are interpreted as left and bottom values, if four numbers are given, they are interpreted as left, bottom, right, top</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Defines the size of figure</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>If set, no legend is drawn</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>Defines the position of the legend; default: matplolib default</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

### Interaction Options

If one of the scripts is simply started with no options that are listed below, the figure will be shown. To write the figure additionally into a file, the filename to generate must be given using the (or for short).

If the script is run in a batch file, it is often not convenient to show the figure (once known it is as it should be). In such cases, the option () can be used that suppresses showing the figure.

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
<td><p>Defines the name under which the figure shall be saved</p></td>
</tr>
<tr class="even">
<td>
<p><br />
</p></td>
<td><p>If set, the figure will not be shown</p></td>
</tr>
<tr class="odd">
</tr>
</tbody>
</table>

Outdated
========

The tools are meant to be named as following: <API>_<DATA>_<DESCRIPTION>.py, where:

-   *<API>*: mpl for matplotlib
-   *<DATA>*: the SUMO-output that is processed (mainly)
-   *<DESCRIPTION>*: what the tool does

mpl_dump_twoAgainst.py
------------------------

Reads two dump files (mandatory options and , or, for short and ). Extracts the value described by (default: *speed*). Plots the values of dump2 over the according (same interval time and edge) values from dump1.

Either shows the plot (when is set) or saves it into a file (when is set).

You can additionally plot the normed sums of the value using (). In the other case, you can try to use to assign different colors to the read intervals.

You can format the axes by using and and set theit limits using and . The output size of the image may be set using .

mpl_tripinfos_twoAgainst.py
-----------------------------

Reads two tripinfos files (mandatory options and , or, for short and ). Extracts the value described by (default: *duration*). Plots the values of tripinfos2 over the according (same vehicle) values from tripinfos1.

Either shows the plot (when is set) or saves it into a file (when is set).

You can format the axes by using and and set theit limits using and . The output size of the image may be set using .

mpl_dump_timeline.py
----------------------

Reads a value (given as , default *speed*) for edges defined via from the dumps defined via . Plots them as time lines, using the colors defined via . Please note that the number of colors must be equal to number of edges \* number of dumps.

Either shows the plot (when is set) or saves it into a file (when is set).

You can format the axes by using and and set theit limits using and . The output size of the image may be set using .

mpl_dump_onNet.py
-------------------

Reads a network (defined using or ) and an edge-dump file ( or '''-d *<DUMP_FILE>*}}). Plots the network using the geometries read from *<NET>*. Both the width and the colors used for each edge are determined using where both *<WIDTHVALUE>* and *<COLORVALUE>* are attributes within the dump-file that exist for each edge.

You can change the used color map by setting . *<DEFINITION>* is made of a sorted list of values (between 0 and 1) and assigned colors. This means that the default *0:\#ff0000,.5:\#ffff00,1:\#00ff00* let streets with low value for *<COLORVALUE>* appear red, for those in the middle yellow and for those with a high value green. For values between the given values, the color is determined using linear interpolation. Please note that only lowercase hexadecimal characters may be used.

Either shows the plot (when is set) or saves it into a file (when is set).

sums up the values found for each edge and divides the result by the number of these values. If join is not set and is given, one should choose an output name which looks as following: *<NAME>%05d*.png. The *%05d* will be replaced by the current time step written.

If you have generated a set of images by not “joining” (aggregating) the data, you can convert the obtained pictures into an animated gif using ImageMagick and the following command:

`convert -delay 20 *.png -loop 0 animation.gif`

(loop 0 means that the animation repeats from begin after the end)

You can format the axes by using and and set theit limits using and . The output size of the image may be set using .