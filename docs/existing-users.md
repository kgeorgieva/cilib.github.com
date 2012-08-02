---
layout: docs
title: "Moving to SBT: A Guide for Existing Users"
group: "docs"
---
{% include JB/setup %}

Current users of CIlib will notice that CIlib has been 
[split into two parts](/2012/07/16/removal-of-simulator-scripts/index.html):
the library, containing all the algorithms, problems, etc., and the simulator, 
containing all simulation related code.

This means that a number of things change with regards to the location of files
and compiling:

- The XML files have moved from /xml to /simulator/xml
- The output jar file is now named `simulator-assembly-0.8-SNAPSHOT.jar` and is placed
in /simulator/target when compiled
- To compile the jar file `sbt assembly` is used instead of `mvn`
(note: if you run `sbt` and type `~assembly` then SBT will automatically compile and 
test CIlib whenever changes are saved to any file in the CIlib sources).

The instructions on the [developer's getting started page](dev/getting-started.html)
can also be followed if there is any trouble with the new changes as they may also apply.

