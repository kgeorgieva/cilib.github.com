---
layout: docs
title: "Getting Started in Linux"
group: "dev-docs"
description: ""
---
{% include JB/setup %}

The following instructions will help you get CIlib running in a few simple steps.
Note that these instructions are for *nix environments.

### Step 1: Install the required programs

In order to start developing with CIlib a number of programs are required. In
addition to these it is also recommended to have Scala 2.9.x installed.

#### Install SBT version 0.11.3-2 or later

SBT (Simple-build-tool) is the build tool used by CIlib. Install it by
following the instructions on the SBT 
[Getting Started page](https://github.com/harrah/xsbt/wiki/Getting-Started-Setup), 
or install it through your distro's package manager if it is available.

Make sure SBT is setup correctly by typing the following on the command line:

    $ sbt --version

The output should be similar to "sbt launcher version 0.11.3-2."

#### Install Git

Git is the source version control system used by CIlib.
Follow the instructions [here](http://git-scm.com/book/en/Getting-Started-Installing-Git)
to install Git, or install it through your distro's package manager if it is available.

Make sure Git is setup correctly by typing the following on the command line:

    $ git --version

The output should be similar to "git version 1.7.9.5."


### Step 2: Get the source code

If you want to contribute to CIlib you will need [Github account](https://github.com/signup/free).

Once you have an account fork the CIlib repository by clicking the "Fork" button
on the top right of the [CIlib Github page](https://github.com/cilib/cilib)

Once you have forked the repository you need to clone it to your local machine.
Start by creating a folder where the source code will be placed e.g.

    $ mkdir ~/cilib

then clone your repository with

    $ git clone http://github.com/USERNAME/cilib.git ~/cilib

where USERNAME is your Github username and ~/cilib is the folder you created for the source code.
Once everything is downloaded, add the CIlib repository as an upstream remote repository:

    $ git remote add upstream http://github.com/cilib/cilib.git

The CIlib library code is in the library folder and the simulator and example XML 
files are in the simulator and simulator/xml folders respectively.

### Step 3: Compile CIlib

Compile CIlib using SBT by changing to CIlib's source directory

    $ cd ~/cilib

and running SBT with the clean, compile and assemble commands

    $ sbt
    > clean
    > assembly
    > exit

These steps will download all the dependencies and may take some time to finish.
The final assembled jar is placed in `~/cilib/simulator/target/` and is called 
`simulator-assembly-0.8-SNAPSHOT.jar`


### Step 4: Set up a running script and test

Create a file called `simulator.sh` and place the following in the file:

{% gist 3122738 %}

`${CILIB_ASSEMBLY}` is the location of the assembled CIlib jar file (in this case
`~/cilib/simulator/target/simulator-assembly-0.8-SNAPSHOT.jar` and `${JAVA_OPTS}` 
are options sent to java mainly for memory management e.g. `-Xms512m -Xmx2g`.

Make sure the file is executable and on the system path with the following:

    $ chmod +x path/to/simulator.sh
    $ export PATH=$PATH:path/to/simulator

Note that the export command is only applicable to your current session and will
be reset when you exit the command line. To make the change permanent consult the
documentation for your particular distro regarding environment variables.

Finally test the simulator script with the following:

    $ simulator.sh ~/cilib/simulator/xml/ga.xml

If no errors occurred CIlib has been successfully set up. If, while running the
simulation, a FileNotFoundException is thrown it may be because the output file 
name contains a folder name in it. Just create the folder and run the simulation
again. Keep this in mind when running future simulations.


### Step 5 (Optional): Set up your IDE

- [Netbeans](netbeans.html)
- Eclipse
- IDEA


### Proxy Issues
- If SBT cannot fetch the dependencies because of proxy authentication then follow
the instructions in the "HTTP Proxy" section of the [SBT Setup Notes](https://github.com/harrah/xsbt/wiki/Setup-Notes)

- For proxy issues using Git refer to 
[this Stack Overflow question](http://stackoverflow.com/questions/7734518/how-to-set-up-git-to-get-through-a-proxy)
which contains a number of different solutions.

