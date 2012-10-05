---
layout: docs
title: "Getting Started on the Cilib Website"
group: "dev-docs"
description: ""
category: updates
tags: [cilib, configuration, git, sbt, ruby, jekyll, windows]
---
{% include JB/setup %}

This document describes how to configure all the software required to develop the 
CILib website in Windows 7.

## Configuration for development of the Cilib Website

### Install Ruby and Ruby Development Kit
Download and install the latest version of Ruby from: [Ruby](http://rubyinstaller.org/downloads/).

Download and install the latest version of DevKit from: [Ruby](http://rubyinstaller.org/downloads/).

Right click on Computer > Properties > Advanced System Settings > Environment Variables and
add the path for the \bin directories of both, Ruby and DevKit, to your PATH variable (in windows
the different paths are separated by a semicolon ";").

Open command line, navigate to the directory of the Ruby Development kit and type:

    ruby dk.rb init
    ruby dk.rb install


### Install Rdiscount
To install this type the following into command line:

    gem install -p http://username:password@proxy:port rdiscount

Note: This is if you are working through a proxy. If you are not working through a proxy, remove "http://username:password@proxy:port" from the above command

### Install Jekyll
If ruby has been installed correctly, then typing the following into command line will install jekyll:

    gem install -p http://username:password@proxy:port jekyll

Note: This is if you are working through a proxy. If you are not working through a proxy, remove "http://username:password@proxy:port" from the above command

### Clone the Repository
This is the same process as cloning the CILib repository:

    git clone URLFromGitHub nameOfFolderToCloneTo
    git remote add upstream https://github.com/cilib/cilib.github.com.git

### Build
To build the site navigate to the site's file location and type:

    rake preview

You may also use:

    jekyll --server

### To View
To view the site open your browser and navigate to:

    http://localhost:4000

If there are any questions join us on [irc chat](http://webchat.freenode.net/?channels=cilib).
