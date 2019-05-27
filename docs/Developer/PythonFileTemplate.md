---
layout: post
title: Developer PythonFileTemplate
permalink: /Developer/PythonFileTemplate/
---

`#!/usr/bin/env python # Leave this one out for non executable python files`
`# -*- optional encoding line, use if non-ASCII characters are in the code -*-`
`# Eclipse SUMO, Simulation of Urban MObility; see `[`https://eclipse.org/sumo`](https://eclipse.org/sumo)
`# Copyright (C) `<YEAR OF CREATION>`-`<CURRENT YEAR>` German Aerospace Center (DLR) and others.`
`# This program and the accompanying materials`
`# are made available under the terms of the Eclipse Public License v2.0`
`# which accompanies this distribution, and is available at`
`# `[`http://www.eclipse.org/legal/epl-v20.html`](http://www.eclipse.org/legal/epl-v20.html)
`# SPDX-License-Identifier: EPL-2.0`
`# @file    `<FILENAME>
`# @author  `<AUTHOR'S NAME, ONE SEPARATE LINE FOR EACH AUTHOR>
`# @author  `<AUTHOR'S NAME 2>
`# @date    `<FILE CREATION DATE>
`# @version $Id: $`
“`"`”
<A BRIEF DESCRIPTION OF THE FILE'S CONTENTS>
<more documentation including examples>
“`"`”
`from __future__ import print_function`
`from __future__ import absolute_import`
`import os`
`import sys`
`import ...`
`sys.path.append(os.path.join(os.environ[`“`SUMO_HOME`”`], 'tools'))`
`import sumolib  # noqa`