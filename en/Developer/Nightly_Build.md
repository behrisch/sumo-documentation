---
layout: post
title: Developer Nightly Build
permalink: /Developer/Nightly_Build/
---

There are two main scripts responsible for the nightly build process which are (for the linux part) and for Windows. Essentially they both perform the following steps:

1.  git pull
2.  do a clean build (release and debug version)
3.  run unittests (currently linux only)
4.  build and upload packages
5.  build and upload documentation (linux only)
6.  run the acceptance tests (texttest)
7.  upload test results

All the results can be found in the [daily dir on the sumo web space](http://sumo.dlr.de/daily/), also see [Downloads\#Nightly_Snapshots](/Downloads#Nightly_Snapshots "wikilink"). Coverage information based on running the nightly tests is generated as well. The status can be found at [the sumo web space](http://sumo.dlr.de/daily/lcov/html/).

There is also a local copy in the Daten/Sumo/daily directory (including the most recent game scenarios) the DLR internal tsall NAS. The windows script uses the sumo-all package from the local dir to build the binary distributable zip and the game zip.

One final step is to trigger the nightly build on the opensuse build service. This is achieved via uploading a new spec file via a cronjob, which triggers an automatic download of the sources and a rebuild. All errors and test result e-mails are directed to the sumo-tests list at dlr.de, except for the build service errors which go to a private account since the build is currently in a private project.

Additionally there is a continuous integration build for MacOS on Travis: <https://travis-ci.org/DLR-TS/sumo>.

Platforms and tests
-------------------

-   “sumo” refers to the publicly available sumo
-   “meso” means the variant with embedded python, OSG and FFMPEG running mesoscopic and python3 tests
-   the clang build has debugging code enabled via the configure option “--enable-debug”

| variant | platform      | start time    | estimated duration |
|---------|---------------|---------------|--------------------|
| sumo    | 32 bit msvc10 | 02:00         | 1h                 |
| sumo    | 64 bit msvc10 | (after 32bit) | 1h                 |
| meso    | 32 bit msvc10 | 05:00         | 1h                 |
| meso    | 64 bit msvc10 | (after 32bit) | 1h                 |
| sumo    | 32 bit gcc    | 19:00         | 3h                 |
| sumo    | 64 bit gcc    | 23:30         | 1.5h               |
| meso    | 64 bit gcc    | 22:30         | 0.5h               |
| sumo    | 64 bit clang  | 09:00         | 1.5h               |
| meso    | 64 bit clang  | 11:00         | 1.5h               |

Scenario tests
--------------

-   “scenario” refers to the internal tests available at source:trunk/tests and includes the default and the daily tests
    -   “weekly” are the weekly test suites of the internal tests available at source:trunk/tests
    -   all scenario tests run with the internal (meso) variant of sumo
-   “ics” refers to the iCS tool of colombo (currently disabled)
-   “vabene” refers to the tests in the vabene repository (currently disabled)

| variant         | platform     | start time         | estimated duration |
|-----------------|--------------|--------------------|--------------------|
| scenario        | 64 bit gcc   | 02:00              | 5h ?               |
| scenario weekly | 64 bit gcc   | 02:00 (only sa)    | 72h ?              |
| scenario        | 64 bit clang | 02:00 (only mo-fr) | 8h ?               |

