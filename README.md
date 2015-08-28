How to setup python environment on Mac OS X Yosemite & El Capitan
=============

On this page I describe how to setup `python` environment on `Mac OS X Yosemite (10.10)` and `El Capitan (10.11)`


Know issues
----------

Nothing yet.


HomeBrew
----------

Before you start, open `Terminal` application and install **Xcode command-line tool**. It's required to install a lot of software on your Mac.

```
xcode-select --install
```

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
- `zookeeper --with-python`
- `boost --with-python`
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

- `brew install python` installs `python` and `pip`
- `pip install virtualenv`
- `pip install virtualenvwrapper`


### Django completion

Add autocompletion in terminal when we type `manage.py` or `django-admin.py` and press `<tab>` key two times

- `cd /usr/local/etc/bash_completion.d/`
- `wget https://raw.github.com/django/django/master/extras/django_bash_completion`
- `source ~/.profile` to affect changes


Post-installation
----------

- create virtual environments for projects `mkvirtualenv [env_name]` and run `pip install -r requirements.txt`
- restore MySQL databases
- restore mongodb collections: 1. `mongodump --out backup/` 2. `mongorestore backup/`


Python 3 support
---

To create virtual environment with `python3` support you need to specify path to specific version of python.

```shell
$ which python3
/usr/local/bin/python3
$ mkvirtualenv -p /usr/local/bin/python3 project_name
```


Software
----------

This is my list of sofrware that I use:

- From App Store: Pages, Numbers, Keynote, Pixelmator, iDraw, 1Password, The Unarchiver, Pocket
- [DropBox](https://www.dropbox.com)
- [Skype](http://www.skype.com)
- [Google Chrome](http://www.google.com/chrome)
- [SourceTree](http://www.sourcetreeapp.com)
- [MySQL Workbench](http://dev.mysql.com/downloads/workbench/)
- [Sublime Text 3](http://www.sublimetext.com/3)
- [Atom](https://atom.io)
- [VirtualBox](https://www.virtualbox.org)
- [TunnelBlick](https://code.google.com/p/tunnelblick/) - graphical OpenVPN for Mac
- [uTorrent](http://www.utorrent.com) - torrent client
- [Team Viewer](http://www.teamviewer.com/en/index.aspx) - share your screen
- [Google Music Manager](https://support.google.com/googleplay/answer/1229970) - upload music to Google Play
- --- optional ---
- [XMind](http://www.xmind.net) - save your minds in graphical representation
- [Inkspape](http://www.inkscape.org/en/) - free vector graphic tool. Require to install [XQuartz](http://xquartz.macosforge.org/landing/)
- [VLC Video Player](http://www.videolan.org/vlc/download-macosx.html)


Setup OS X integration with web sites
----------

- Login to [google.com](http://google.com) and auto-setup OS X to work with: mail, calendar, etc
- Login to [facebook](http://facebook.com), [twitter](http://twitter.com) and [linkedin](http://linkedin.com) and allow auto-setup OS X
- Login to [github](http://github.com) and [bitbucket](http://bitbucket.org)


Read also
----------

- [How to configure Atom editor on Yosemite](https://github.com/1st/python-on-osx/blob/master/ATOM.md)
