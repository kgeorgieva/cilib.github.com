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

### Using GIT

If you are working with a proxy, you need to configure the proxy settings. To do that
type the following line onto command line:

    git config --global http.proxy http://username:password@proxy:port

To clone a repository tye the following:

    git clone URLFromGitHub nameOfFolderToCloneTo


## For development of the CILib Website

### Install Ruby and Ruby Development Kit
Download and install the latest version of Ruby from: http://rubyinstaller.org/downloads/

Download and install the latest version of DevKit from: http://rubyinstaller.org/downloads/

Right click on Computer > Properties > Advanced System Settings > Environment Variables and
add the path the \bin directories of both, Ruby and DevKit, to your PATH variable (in windows
the different paths are separated by a semicolon ";").

Open command line and do the following:
- Go to the directory of the Ruby Development kit
- type: ruby dk.rb init
- type: ruby dk.rb install


### Install Rdiscount
To install this type the following into command line:

    gem install -p http://username:password@proxy:port rdiscount


### Install Jekyll
If ruby has been installed correctly, then typing the following into command line will install jekyll

    gem install -p http://username:password@proxy:port jekyll


### Build
To build the site navigate to the site's file location and type:

    rake preview

### To Generate
To generate the site type:

    jekyll --server

### To View
To view the site open your browser and navigate to:

    http://localhost:4000

If there are any questions join us on [irc chat](http://webchat.freenode.net/?channels=cilib).
