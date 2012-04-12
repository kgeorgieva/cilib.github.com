# CIlib Documentation #

This repository maintains the source for the CIlib website.

## Contributing ##
....

## Dependencies ##
To generate and view the website locally, [Jekyll](http://jekyllrb.com) is
required. The installation of Jekyll for different operating systems is
described below (but please also reference the instructions at the Jekyll
[wiki](https://github.com/mojombo/jekyll/wiki/Install)).

Note that Jekyll requires [Ruby](http://ruby-lang.org) to be present on the
system.

### Unix ###
Jekyll is installed using either your operating system package manager
(applicable to most Linux distros) or via RubyGems:

    gem install jekyll

### Mac OS X ###
Mac OS X users will need to have XCode, as well as Ruby available on the
system to use Jekyll. OSX users may require an update to RubyGems:

    sudo gem update --system

Follow the instructions for Unix above. If required, the command may require
superuser access, so prepend the commands with `sudo`.

### Windows ###
Get Ruby installed on the system using the [RubyInstaller](http://rubyinstaller.org/downloads)
You should use the 1.8.x release if 1.9.x causes you problems with unicode.

Follow the instructions for the [RubyInstaller DevKit](https://github.com/oneclick/rubyinstaller/wiki/Development-Kit)

Install Jekyll using gem:

    gem install jekyll

## Building and Viewing ##
cd into the `cilib.github.com` repository directory and build using:

    jekyll --server

The generated site is available at `http://localhost:4000`

## Markdown ##
As per the default used by Jekyll, this site uses [Maruku](http://maruku.rubyforge.org/maruku.html) extensions.

## License ##
...
