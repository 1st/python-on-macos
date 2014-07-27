How to setup python environment on Mac OS X Yosemite
=============

On this page I describe how to setup `python` environment on `Mac OS X Yosemite (10.10)`.

HomeBrew
----------

Install [HomeBrew](http://brew.sh) to have ability to install up-to-date software, like `apt-get install` in `Ubuntu`.

My list of `brew` software (use `brew install [package_name]`):
- memcached
- mercurial
- git
- mysql
- postgresql
- mongodb
- rabbitmq
- node
- wget
- --- optional ---
- zookeeper
- boost --with-python
- lynx
- cairo
- jpeg
- jsoncpp
- gettext
- glib
- libpng
- log4cpp


System changes
----------

Edit `nano ~/.profile` file to have this lines:

```
# load all completions
source /usr/local/etc/bash_completion.d/*
# load virtual env wrapper
source virtualenvwrapper.sh
# Set architecture flags
export ARCHFLAGS="-arch x86_64"
# Ensure user-installed binaries take precedence
export PATH=/usr/local/bin:$PATH
# Load .bashrc if it exists
test -f ~/.bashrc && source ~/.bashrc
```

Press `Cmd + O` to save file, `Cmd + X` to exit from nano. Run this command in terminal `source ~/.profile` to load changes.

Edit `~/.hgrc` and insert info about my user:

```
[ui]
username = User Name <user@gmail.com>
```

Python tools
----------

- brew install python
- pip install virtualenv
- pip install virtualenvwrapper


Post-installation
----------

- create virtual environments for projects `mkvirtualenv [env_name]` and run `pip install -r requirements.txt`
- restore MySQL databases
- restore mongodb collections


Software
----------

This is my list of sofrware that I use:

- From App Store: Pages, Numbers, Keynote, Pixelmator, iDraw, 1Password, The Unarchiver, Pocket
- DropBox
- Skype
- Google Chrome
- SourceTree
- MySQL Workbench
- Sublime Text 3
- Atom
- VirtualBox
- TunnelBlick
- uTorrent
- Team Viewer
- Google Music Manager
- --- optional ---
- XMind
- Inkspape, XQuartz
- LVC Video Player


Setup OS X integration with web sites
----------

- Login to google.com and auto-setup OS X to work with: mail, calendar, etc
- Login to facebook and auto-setup OS X
- Login to twitter and auto-setup OS X
- Login to linkedin and auto-setup OS X
- Login to github and bitbucket
