---
layout: post
title: "Windows Configuration"
description: ""
category: updates
tags: [cilib, configuration, git, sbt, ruby, jekyll, windows]
---
{% include JB/setup %}

This document describes how to configure all the required software for CIlib and the
CILib website in Windows 7. It includes details for users with proxy settings and for
users that do not require proxy access.

## GIT

### Downloading and installing Git
Download Git from [Git](http://git-scm.com/download).

Make sure that you select: Run Git from Windows Command Prompt while installing.

Open command line (Start > cmd).

Configure git with name and address:

    git config --global user.name "Your Name" 
    git config --global user.email your@email.address

Test with: git --version.

### Github

Resister an account with [Github](https://github.com/).


### Getting the source code

Go to the [CIlib Repository](https://github.com/cilib/cilib) and click on Fork located 
on the top right.

### Cloning the Repository

If you are working with a proxy, you need to configure the proxy settings. To do that
type the following line onto command line:

    git config --global http.proxy http://username:password@proxy:port

To clone a repository tye the following:

    git clone URLFromGitHub nameOfFolderToCloneTo

Add the CIlib repository as an upstream remote repository:

    git remote add upstream https://github.com/cilib/cilib.git

One possibly useful link: [Stack Overflow post](http://stackoverflow.com/questions/67699/how-do-i-clone-all-remote-branches-with-git)


### Using Git

To create branch based on another, checkout the branch that you need as a base:

    git branch newBranch

To checkout a branch:

    git checkout branchName

To see list of branches:

    git branch

To see modified untracked files:

    git status

To add a change:

    git add <path>

To remove change:

    git rm <path>

To commit changes:

    git commit

- Add description of changes.
- To save press Esc and type ":x" to save and exit VIM.

To push changes to repository"

    git push origin branchName

- Git will ask for your github.com password.

To fetch changes from origin:

    git checkout master
    git fetch upstream
    git merge upstream/master


## Netbeans and Scala plugin

Follow the instructions listed in Step 1 found at: 
[Getting Started](http://cilib.net/2012/07/18/netbeans-cilib-and-sbt/).
Make sure that you have the latest version of Netbeans to avoid running 
into trouble (At the time that this was documented Netbeans 7.2 was used).

## SBT

Download the .msi provided here: [SBT](http://www.scala-sbt.org/).

Right click on Computer > Properties > Advanced Settings > Environment Variables.
Add the following to your user variable: path, where ~ is the path to the sbt.bat:

    ~/sbt.bat

- If the System path variable also exists, only add ~ to the it.

Go to the folder: C:\Users\YourUser\.sbt.

Create the folder "plugins" if it does not exist.

Inside this folder create the file plugins.sbt if it does not exist.

Add the following to the file and save it (note the empty lines in between):

    resolvers += ScalaToolsSnapshots

    resolvers += "remeniuk repo" at "http://remeniuk.github.com/maven"

    libraryDependencies += "org.netbeans" %% "sbt-netbeans-plugin" % "0.1.4"

If there is a proxy, find the sbt.bat file located in the cilib folder and type:

    -Dhttp.proxyHost=proxy -Dhttp.proxyPort=port -Dhttp.proxyUser=username -Dhttp.proxyPassword=password

- between "%_JAVACMD%" and %_JAVA_OPTS% which are found after ":run".

Open command line and type:

    sbt

Then type:

    netbeans

Navigate to your cilib folder if not already there and use the following to compile:

    sbt compile

Use the following to build the project

    sbt assembly

Use the following to run simulations, where xml has the configuration of the experiments:

    simulator.bat simulator/xml/ga.xml

Follow the instructions listed in Step 4 found at: 
[Getting Started](http://cilib.net/2012/07/18/netbeans-cilib-and-sbt/).

## For development of the CILib Website

### Install Ruby and Ruby Development Kit
Download and install the latest version of Ruby from: [Ruby](http://rubyinstaller.org/downloads/).

Download and install the latest version of DevKit from: [Ruby](http://rubyinstaller.org/downloads/).

Right click on Computer > Properties > Advanced System Settings > Environment Variables and
add the path the \bin directories of both, Ruby and DevKit, to your PATH variable (in windows
the different paths are separated by a semicolon ";").

Open command line, navigate to the directory of the Ruby Development kit and type:

    ruby dk.rb init
    ruby dk.rb install


### Install Rdiscount
To install this type the following into command line:

    gem install -p http://username:password@proxy:port rdiscount


### Install Jekyll
If ruby has been installed correctly, then typing the following into command line will install jekyll:

    gem install -p http://username:password@proxy:port jekyll


### Build
To build the site navigate to the site's file location and type:

    rake preview

You may also use:

    jekyll --server

### To View
To view the site open your browser and navigate to:

    http://localhost:4000

If there are any questions join us on [irc chat](http://webchat.freenode.net/?channels=cilib).