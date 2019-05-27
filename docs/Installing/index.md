---
layout: post
title: Installing
permalink: /Installing/
---

Windows
=======

There are four different binary packages for Windows depending on the platform (32 vs. 64 bit) you have and what you want to do with SUMO. If you want to install it locally and have administrator rights on your machine you should download and execute one of the installers (preferably 64 bit). If you need a “portable” version or do not have admin rights, use the correct zip, extract it into a desired folder using [7Zip](http://7-zip.de/), [Winzip](http://www.winzip.de/prod_down.htm), or a similar tool. Every package contains the binaries, all dlls needed, the examples, tools, and documentation in HTML format.


Download 64 bit installer: \[<http://prdownloads.sourceforge.net/sumo/sumo-win64-%7B%7BVersion%7D>}.msi?download sumo-win64-.msi\]

Download 64 bit zip: \[<http://prdownloads.sourceforge.net/sumo/sumo-win64-%7B%7BVersion%7D>}.zip?download sumo-win64-.zip\]

Download 32 bit installer: \[<http://prdownloads.sourceforge.net/sumo/sumo-win32-%7B%7BVersion%7D>}.msi?download sumo-win32-.msi\]

Download 32 bit zip: \[<http://prdownloads.sourceforge.net/sumo/sumo-win32-%7B%7BVersion%7D>}.zip?download sumo-win32-.zip\]

Within the installation folder, you will find a folder named “**bin**”. Here, you can find the executables (programs). You may double click on [SUMO-GUI](/SUMO-GUI "wikilink") and take a look at the examples located in **data/examples**. All other applications ([DUAROUTER](/DUAROUTER "wikilink"), [DFROUTER](/DFROUTER "wikilink"), etc.) have to be run from the command line. To facilitate this there is also a start-commandline.bat which sets up the whole environment for you. If you feel unsure about the command line, please read [Basics/Basic_Computer_Skills\#Running_Programs_from_the_Command_Line](/Basics/Basic_Computer_Skills#Running_Programs_from_the_Command_Line "wikilink").

If you want a bleeding edge nightly build or need tests or source files, you can download them from the [Download](/Downloads "wikilink") page.

For building SUMO from source see [building SUMO under Windows](/Installing/Windows_Build "wikilink").

Linux
=====

If you run debian or ubuntu, SUMO is part of the regular distribution and can be installed like this:

`sudo apt-get install sumo sumo-tools sumo-doc`

If you need a more up-to-date ubuntu version, it may be found in a separate ppa, which is added like this:

`sudo add-apt-repository ppa:sumo/stable`
`sudo apt-get update`

and then again

`sudo apt-get install sumo sumo-tools sumo-doc`

Precompiled binaries for different distributions like openSUSE and Fedora can be found at these [repositories for binary Linux versions](http://download.opensuse.org/repositories/home:/behrisch/). These repositories contain nightly builds as well. In the case your system is not listed here or you need to modify the sources, [you have to build SUMO from sources](/Installing/Linux_Build "wikilink").

MacOS
=====

SUMO can be found in the [Macports repositories](https://www.macports.org). After [installing Macports](https://www.macports.org/install.php) (this also needs XCode and its command line tools as well as an Apple Developer ID) make sure that an X server was installed ([XQuartz](http://xquartz.macosforge.org/) worked here) and that you have a terminal application like [iTerm2](https://www.iterm2.com/) ready. Now start a terminal session and run

`sudo port install sumo`

If you need a more recent SUMO version or want to modify the sources you should do the above Macports installation as well to have all the dependencies ready. Afterwards you can follow the instructions of the [Linux build](/Installing/Linux_Build#Getting_the_source_code "wikilink") with some additions for [macOS](/Installing/MacOS_Build "wikilink").

A guid for a homebrew based installation is given [here](/Installing/MacOS_Build_w_Homebrew "wikilink").

via Docker
==========

Building and installing SUMO from source is not an easy task for beginner users. Docker is a popular tool to solve this issue. Searching “SUMO” at [Docker Hub](https://hub.docker.com) will give several results from existing attempts at Dockerising SUMO.

The solution given at [docker-sumo](https://github.com/bogaotory/docker-sumo) demonstrates how to Dockerise SUMO version 0.30.0 on top of Ubuntu 16.04. As well as **sumo** and **traci**, the use of **sumo-gui** is also demonstrated by [docker-sumo](https://github.com/bogaotory/docker-sumo) so that the users have access to the graphical interface of a Dockerised SUMO.