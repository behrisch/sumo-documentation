---
title: Tutorials Plotting Cookbook
permalink: /Tutorials/Plotting_Cookbook/
---

In the following, You will find some examples for plotting results obtained from SUMO.

Number of Vehicles within the Simulation over Time
--------------------------------------------------

Let's assume You want to show the number of vehicles running through your simulation over time. You'll need the [summary-output](/Simulation/Output/Summary "wikilink") that contains the number of vehicles within the simulation for each simulation time step.

If Your [summary-output](/Simulation/Output/Summary "wikilink") is named “summary.xml”, You may show the number of running vehicles using

`python plot_summary.py -i summary.xml`

as “<span class="inlxml">running</span>”, the measurement You want to plot, is the default. The following image will be shown:

[300px](/Image:summary_running_mo.png "wikilink")

Now, let's assume You want to compare the number of running vehicles from different runs. The example below uses [summary-outputs](/Simulation/Output/Summary "wikilink") from runs that cover different types of days of a week (mo\\summary.xml: Monday, dido\\summary.xml: Tuesday-Tursday, etc.). As we want to show only a single day, we limit the x-axis to \[0,86400\] (86400: seconds in a day) using and we also save the figure into the file “summary_running_all.png” using . To know what is shown, we replace the file names in the legend by the week day types using .

`python plot_summary.py -i mo\summary.xml,dido\summary.xml,fr\summary.xml,sa\summary.xml,so\summary.xml \`
` -l Mo,Di-Do,Fr,Sa,So -o summary_running_all.png --xlim 0,86400`

[300px](/Image:summary_running_all.png "wikilink")

Ok, now we'll make it professional by adding labels and titles, proper ticks, using a different format for the simulation time than seconds, etc.

`python plot_summary.py -i mo\summary.xml,dido\summary.xml,fr\summary.xml,sa\summary.xml,so\summary.xml \`
` -l Mo,Di-Do,Fr,Sa,So --xlim 0,86400 --ylim 0,10000 -o sumodocs/summary_running.png --yticks 0,10001,2000,14 \`
` --xticks 0,86401,14400,14 --xtime1 --ygrid --ylabel `“`running`` ``vehicles`` ``[#]`”` --xlabel `“`time`”` \`
` --title `“`running`` ``vehicles`` ``over`` ``time`”` --adjust .14,.1 `

[300px](/Image:summary_running.png "wikilink")

The [summary-output](/Simulation/Output/Summary "wikilink") contains further measures that can be visualised in the same way, among them <span class="inlxml">loaded</span>, <span class="inlxml">inserted</span>, <span class="inlxml">waiting</span>, or <span class="inlxml">ended</span>. Please consult the [summary-output](/Simulation/Output/Summary "wikilink") documentation for a complete list.

Further information can be found at:

-   [summary-output](/Simulation/Output/Summary "wikilink") documentation
-   [visualisation tools](/Tools/Visualization "wikilink") documentation
