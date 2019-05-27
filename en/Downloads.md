---
layout: post
title: Downloads
permalink: /Downloads/
---

Here, you will find SUMO both as sources and as compiled binaries.

Please [contact](/Contact "wikilink") us if you have any problems. If you want to report a bug, please [open a GitHub issue](https://github.com/DLR-TS/sumo/issues/new). For further information about the changes between releases see the [ChangeLog](/ChangeLog "wikilink").

SUMO is licensed under the [EPL-2.0](https://eclipse.org/legal/epl-v20.html) using only [open source libraries](/License "wikilink").

Packages
--------

SUMO is available as different packages. The contents of each package is listed in the table below.

<table>
<thead>
<tr class="header">
<th></th>
<th><p>bin</p></th>
<th><p>build</p></th>
<th><p>src<br />
(source<br />
code)</p></th>
<th><p>user<br />
docs</p></th>
<th><p>developer<br />
docs<br />
(doxygen)</p></th>
<th><p>data</p></th>
<th><p>examples</p></th>
<th><p>tutorials</p></th>
<th><p>tests</p></th>
<th><p>tools (except jars)</p></th>
<th><p>jars</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>sumo-src-<em>XXX</em>.tar.gz<br />
sumo-src-<em>XXX</em>.zip</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>sumo-doc-<em>XXX</em>.tar.gz<br />
sumo-doc-<em>XXX</em>.zip</p></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>sumo-tests-<em>XXX</em>.tar.gz<br />
 </p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>sumo-win??-<em>XXX</em>.zip<br />
 </p></td>
<td><p>X</p></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>sumo-win??-<em>XXX</em>.msi<br />
 </p></td>
<td><p>X</p></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>sumo-all-<em>XXX</em>.tar.gz<br />
sumo-all-<em>XXX</em>.zip</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>rpm<br />
 </p></td>
<td><p>(X)</p></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

### Repositories

In addition to the open build service, there are a debian and an ubuntu launchpad project in the making:

-   <https://build.opensuse.org/project/show?project=home%3Abehrisch>
-   <http://anonscm.debian.org/gitweb/?p=debian-science/packages/sumo.git>
-   <https://launchpad.net/~sumo>

To add sumo to your ubuntu (11.04 and later) you will need to do:

`sudo add-apt-repository ppa:sumo/stable`
`sudo apt-get update`
`sudo apt-get install sumo sumo-tools sumo-doc`

This is still an experimental feature, feedback is welcome.

SUMO - Latest Release (Version )
--------------------------------

**Release date: 19.12.2017**

-   The latest MS Windows binaries.


Contains the binaries (32 bit), all dlls needed, the examples, tools, and documentation in HTML format.

Download as installer: \[<http://prdownloads.sourceforge.net/sumo/sumo-win32-%7B%7BVersion%7D>}.msi?download sumo-win32-.msi\]

Download as zip: \[<http://prdownloads.sourceforge.net/sumo/sumo-win32-%7B%7BVersion%7D>}.zip?download sumo-win32-.zip\]

Download 64 bit zip: \[<http://prdownloads.sourceforge.net/sumo/sumo-win64-%7B%7BVersion%7D>}.zip?download sumo-win64-.zip\]

Download 64 bit installer: \[<http://prdownloads.sourceforge.net/sumo/sumo-win64-%7B%7BVersion%7D>}.msi?download sumo-win64-.msi\]

-   Linux binaries are created by the [open build service](http://en.opensuse.org/Build_Service)


If the repositories do not contain the libraries (like proj and gdal) they are either part of the distribution or you will need them from another repository (you may try one of the build service repositories here too, e.g. [Application:Geo](http://download.opensuse.org/repositories/Application:/Geo/)). At the moment there is no documentation included in the packages. The repositories include a nightly build as well (called sumo_nightly).

-   [openSUSE Leap 42.1 repository](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_42.1/)
-   [openSUSE Leap 42.2 repository](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_42.2/)
-   [openSUSE Leap 42.3 repository](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_42.3/)
-   [openSUSE Tumbleweed repository](http://download.opensuse.org/repositories/home:/behrisch/openSUSE_Tumbleweed/)
-   [Fedora 24 repository](http://download.opensuse.org/repositories/home:/behrisch/Fedora_24/)
-   [Fedora 25 repository](http://download.opensuse.org/repositories/home:/behrisch/Fedora_25/)
-   [Fedora 26 repository](http://download.opensuse.org/repositories/home:/behrisch/Fedora_26/)
-   [Fedora 27 repository](http://download.opensuse.org/repositories/home:/behrisch/Fedora_27/)
-   [Fedora Rawhide repository](http://download.opensuse.org/repositories/home:/behrisch/Fedora_Rawhide/)

There are [more Linux RPM repositories](https://build.opensuse.org/repositories/home:behrisch) but in a less well maintained state (CentOS and Scientific missing gdal support for instance) because the opensuse build service does not provide the necessary packages any longer. Ubuntu and Debian users please see above for repository information.

-   The latest source-tarball.


Includes sources, examples, Linux-Makefiles and solution files for MSVC++ 2010 (aka 10.0) and above. Does not contain tests.

Download as:

-   \[<http://prdownloads.sourceforge.net/sumo/sumo-src-%7B%7BVersion%7D>}.tar.gz?download sumo-src-.tar.gz\]
-   \[<http://prdownloads.sourceforge.net/sumo/sumo-src-%7B%7BVersion%7D>}.zip?download sumo-src-.zip\]

-   The latest documentation-tarball. Includes a dump of the user documentation from the wiki as well as source code documentation (doxygen and pydoc).


Download as: \[<http://prdownloads.sourceforge.net/sumo/sumo-doc-%7B%7BVersion%7D>}.tar.gz?download sumo-doc-.tar.gz\]

-   The latest tests-tarball. These tests run with [TextTest](http://www.texttest.org).


Download as: \[<http://prdownloads.sourceforge.net/sumo/sumo-tests-%7B%7BVersion%7D>}.tar.gz?download sumo-tests-.tar.gz\]

-   The latest all-inclusive-tarball. Includes sources, tests and docs but no binaries.


Download as: \[<http://prdownloads.sourceforge.net/sumo/sumo-all-%7B%7BVersion%7D>}.tar.gz?download sumo-all-.tar.gz\]

SUMO - Latest Development Version
---------------------------------

SUMO is under active development. You can find a continuously updated list of bug-fixes and enhancements at our [ChangeLog](/ChangeLog "wikilink"). To make use of the latest features [(and to give us pre-release feedback)](/Contact "wikilink") we encourage you to use the latest version from our [code repository](https://github.com/DLR-TS/sumo/).

### Nightly Snapshots

The code within the repository is [compiled each night](/Developer/Nightly_Build "wikilink"). The following resulting packages can be obtained:

-   <http://sumo.dlr.de/daily/sumo-src-git.tar.gz> (sources)
-   <http://sumo.dlr.de/daily/sumo-src-git.zip> (sources)
-   <http://sumo.dlr.de/daily/sumo-msvc12Win32-git.zip> (windows, 32bit)
-   <http://sumo.dlr.de/daily/sumo-msvc12x64-git.zip> (windows, 64bit)
-   <http://sumo.dlr.de/daily/sumo-tests-git.tar.gz> (tests)
-   <http://sumo.dlr.de/daily/sumo-all-git.tar.gz> (sources, documentation and tests)
-   <http://sumo.dlr.de/daily/sumo-game-msvc12Win32-git.zip> (windows 32bit binaries of the sumo game)
-   <http://sumo.dlr.de/daily/sumo-game-msvc12x64-git.zip> (windows 64bit binaries of the sumo game)
-   <http://sumo.dlr.de/daily/sumo-msvc12Win32-git.msi> (windows installer, 32bit)
-   <http://sumo.dlr.de/daily/sumo-msvc12x64-git.msi> (windows installer, 64bit)

The Linux repositories specified above contain a nightly build as well.

[The corresponding documentation](http://sumo.dlr.de/daily/userdoc) is also visible live including [Doxygen docs](http://sumo.dlr.de/daily/doxygen). Additional artifacts such as [tests results](http://sumo.dlr.de/daily) and [code coverage analysis](http://sumo.dlr.de/daily/lcov/html/) are generated every night.

### Nightly Snapshots alternative download server

All nightly builds are also available at the following alternative locations

-   <http://sumo.sourceforge.net/daily/sumo-src-git.tar.gz> (sources)
-   <http://sumo.sourceforge.net/daily/sumo-src-git.zip> (sources)
-   <http://sumo.sourceforge.net/daily/sumo-msvc12Win32-git.zip> (windows, 32bit)
-   <http://sumo.sourceforge.net/daily/sumo-msvc12x64-git.zip> (windows, 64bit)
-   <http://sumo.sourceforge.net/daily/sumo-tests-git.tar.gz> (tests)
-   <http://sumo.sourceforge.net/daily/sumo-all-git.tar.gz> (sources, documentation and tests)
-   <http://sumo.sourceforge.net/daily/sumo-game-msvc12Win32-git.zip> (windows 32bit binaries of the sumo game)
-   <http://sumo.sourceforge.net/daily/sumo-game-msvc12x64-git.zip> (windows 64bit binaries of the sumo game)
-   <http://sumo.sourceforge.net/daily/sumo-msvc12Win32-git.msi> (windows installer, 32bit)
-   <http://sumo.sourceforge.net/daily/sumo-msvc12x64-git.msi> (windows installer, 64bit)

### Direct repository access

You can get very latest sources directly from our Git repository, see [the FAQ on repository access](/FAQ#How_do_I_access_the_code_repository.3F "wikilink"). Normally, they should compile and complete our test suite successfully. To assess the current state of the build, you may take a look at the [nightly test statistics](http://sumo.dlr.de/daily/).

SUMO - older releases
---------------------

Older releases can be obtained via the [sourceforge download portal](http://sourceforge.net/projects/sumo/files/sumo/)

Dependencies for developers
---------------------------

For the Windows platform you can retrieve all dependencies by cloning this repository <https://github.com/DLR-TS/SUMOLibraries>, if you want to develop with Visual Studio. If you just want to run SUMO, use the binary downloads above which already contain the runtime dependencies.