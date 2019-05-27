---
title: Developer HowToRelease
permalink: /Developer/HowToRelease/
---

Packages
--------

for an overview of created packages and contents see [Downloads](/Downloads "wikilink").

Release steps
-------------

Below, a list of steps that should be done in order to publish a new release is given. All necessary commits which have no ticket of their own may refer to .

### Merge phase

Major changes to the SUMO trunk should end about two weeks before the release data. This refers especially to merges of project branches into the trunk. It is also a good idea to inform the developers of dependent software (traci4j, Veins, VSimRTI, TraaS, SUMOPy etc.) at this stage.

### Freeze phase (Release day - 7)

-   check the sources
    -   compile, try to remove warnings and commit the patches
    -   run [AStyle](/Developer/CodeStyle "wikilink") and commit changed files
    -   check the calendar to update copyright statements
    -   check whether the TraCI version [needs to be incremented](/TraCI/Control-related_commands#Response_0x00:_Version "wikilink") and rebuild TraCI constants in python (tools/traci/rebuildConstants.py)
    -   check whether the network version needs to be incremented and update the value in NWFrame::MAJOR_VERSION. Netconvert tests need to be updated afterwards.
    -   update author information
-   check the regular tests
    -   put special attention to the tests which serve as examples, see tests/examples.txt!
    -   Win64 and gcc4_64 should have no failing tests, the other platforms are less important
    -   If there are failing tests, which are not flagged as known bugs, save them after careful checking or open a ticket and assign a known bug.
    -   recheck/rebuild the test networks (if necessary due to netconvert changes)
    -   check the tests again
-   check the documentation
    -   update the [change log](/ChangeLog "wikilink")
    -   generate options documentation from configuration templates using configTemplateToWiki.py (for instance `tools/build/configTemplateToWiki.py activitygen | xclip` which copies it directly to the clipboard)
    -   recheck/rebuild the configuration schemata (if options were added) using tools/xml/rebuildSchemata.py (use the internal build to include all options)
-   check the internal tests (same procedure as above), especially the (to be) published scenarios
-   GitHub
    -   add new [milestone](https://github.com/DLR-TS/sumo/milestones) if necessary
    -   check all remaining tickets and assign them to later milestones or to persons.
-   scenarios (optional)
    -   prepare scenarios for release if the previous version does not run with the current release or significant changes were made to the scenarios
-   update submodules by running `git submodule update` and committing the changes if necessary

The trunk is now frozen. All commits which do not refer to an open ticket for the upcoming release need to be made to a separate branch. The freeze phase should not last longer than one week. The goal is to fix all scenarios and have all failing tests fixed, which are not assigned to a later milestone.

### Release day - 1

All scenarios should be fixed by now.

-   patch the version information
    -   in windows_config.h, also disable the HAVE_VERSION_H macro
    -   in configure.ac and build/wix/sumo.wxs
    -   commit the changes
-   recheck whether submodules changed by doing `git submodule update` and committing the changes after careful inspection
-   check the documentation
    -   update the [change log](/ChangeLog "wikilink") again and include version and release date
    -   modify the [Version Template](/Template:Version "wikilink") to update [download links](/Downloads "wikilink") and .
    -   update the release date on the [main page](/Main_Page "wikilink")

### Release day

The nightly build should have generated all releasable packages. If not, delay the release. (The complete documentation, tests and source distribution build can be achieved via “make dist-complete”.) The following things need to be there:

-   the platform independent part of the distribution;
    -   source distributions (.tar.gz, .zip) (“make dist”, rename)
    -   tests distributions (.tar.gz) (“make dist-tests”)
    -   docs distributions (.tar.gz) (“make dist-doc”)
-   the binary part of the distribution
    -   windows binary distribution (zip, includes docs)
    -   windows installer (msi, Win32 and x64, includes docs)
    -   check presence of RPMs on <https://build.opensuse.org/package/show/home:behrisch/sumo>

If everything is fine:

-   make a new folder in O:\\Daten\\Sumo\\Releases
-   make new sourceforge-release
    -   make a new release within the sumo package (named “version x.y.z”)
    -   add files to the release
    -   change default download attributes
    -   update files at the [opensuse build service](https://build.opensuse.org/package/show?package=sumo&project=home%3Abehrisch)
-   scenarios (optional)
    -   add files to [the scenario folder](https://sourceforge.net/projects/sumo/files/traffic_data/scenarios/)
    -   updated README.txt
-   ~~unpack the doc.tar.gz into the “doc” folder on the web space~~
    -   ~~change the current link for the docs~~
-   inform the users about the new release
    -   post information about the release to sumo-user@eclipse.org and sumo-announce@eclipse.org
    -   ~~post information about the release to news~~
    -   ~~post information into the [blog](http://sumo-sim.org/blog)~~
    -   trigger update of main website at <http://sumo.dlr.de>
-   add a new version tag

`> git tag -a v0_13_7 -m `“`tagging`` ``release`` ``0.13.7,`` ``refs`` ``#563`”
`> git push --tags`

-   close [the milestone](https://github.com/DLR-TS/sumo/milestones) (retargeting open tickets needs to be done manually for now)

### After-release cleanup

The trunk is now open for changes again.

-   reenable HAVE_VERSION_H in windows_config.h
-   rename version to “git” in configure.ac
-   insert a new empty “Git master” section at the top of the [change log](/ChangeLog "wikilink")
-   commit changes
-   drink your favorite beverage
