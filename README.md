How to setup python environment on macOS
=============


On this page I describe how to setup `python` environment on **macOS Catalina (10.13)**.


## Known problems

When I upgrade to a next major version of **macOS** it's almost always some problems appear - some tools stop working, eapecially if you use your system for software development.

- [Virtual env stopped work when I upgraded python via homebrew](#virtual-env-stopped-work-when-i-upgraded-python-via-homebrew)
- [Bad file permissions](#bad-file-permissions)
- [Homebrew doesn't work](#homebrew-doesnt-work)
- [Python doesn't work](#python-doesnt-work)
- [Ruby gems can't be installed](#ruby-gems-cant-be-installed)
- [How to clean unused homebrew dependencies](#how-to-clean-unused-homebrew-dependencies)


## How to setup macOS

- [Install HomeBrew](#homebrew)
- [Do system changes](#system-changes)
- [If you use mercurial](#if-you-use-mercurial)
- [Python setup](#python-setup)
  - [Python virtualenv](#python-virtualenv)
  - [Python 3 support](#python-3-support)
  - [Django completion](#django-completion)
- [Post-installation](#post-installation)
- [Useful software](#useful-software)
  - [Source code editor](#source-code-editor)
  - [Development tools](#development-tools)
  - [Other software](#other-software)
- [Login to web services on macOS](#login-to-web-services-on-macos)
- [Read more](#read-more)

----

## Known problems

### Virtual env stopped work when I upgraded python via homebrew

How to fix a broken virtual env after python version upgrade?

I've created an alias that is easy to use every time when you upgrade the python version via homebrew, and your virtusl env becomes not working. Use it like this `fix_virtualenv <env_name>` and it will auto-fix your python version by replacing a broken links to an actual version of python.

Find the snippet in my [gist](https://gist.github.com/1st/4d8f2bd920cd047ccf1e). Find it by the name `fix_virtualenv`

### Bad file permissions

[Repair disk permissions with Disk Utility](https://support.apple.com/en-us/HT201560). It happens that permissions on some files and directories broken after upgrade to **newer version of macOS**.

Then run next command to make this directory writable:

```shell
sudo chown -R $(whoami) $(brew --prefix)/*
```

Previously it was possible to do like this `sudo chown -R $(whoami):admin /usr/local` but no anymore.

### Homebrew doesn't work

Fix issue with these commands:

```shell
xcode-select --install
cd /usr/local/Library
git pull origin master
```

You can try to find some problems by running:

```shell
brew doctor
```

### Python doesn't work

```shell
brew reinstall python
brew reinstall python@2
```

See also [list of known bugs in HomeBrew](https://docs.brew.sh/Troubleshooting).

### Ruby gems can't be installed

To install ruby gems, use this command:

```shell
sudo gem install -n /usr/local/bin [package]
```

where `[package]` is what you need to install (compass, bundler, etc).

### How to clean unused homebrew dependencies

Command `brew bundle dump` generates a `Brewfile` with all the packages installed by user. Dependent packages are not listed here. It allows to use this file for the next time to install all listed software wiith one command `brew bundle --force cleanup`.

```
brew bundle dump
brew bundle --force cleanup
```

----

## How to setup macOS

### HomeBrew

Before you start, open `Terminal` application and install **Xcode command-line tool**. It's required to install a lot of software on your Mac.

```shell
xcode-select --install
```

Install [HomeBrew](http://brew.sh) to have ability to install up-to-date software, like `apt-get install` in `Ubuntu`.

My list of `brew` software (use `brew install [package_name]`):
- **required**: `memcached`, `git`, `mysql`, `postgresql`, `node`, `wget`
- **optional**: `mercurial`, `mongodb`, `rabbitmq`, `zookeeper --with-python`, `boost --with-python`, `jpeg`, `libpng`


### System changes

Edit `nano ~/.profile` file and insert [this content](https://gist.github.com/1st/4d8f2bd920cd047ccf1e).

Press `Cmd + O` to save file, `Cmd + X` to exit from nano. Run in terminal `source ~/.profile` to load changes.


### If you use mercurial

Edit `~/.hgrc` and insert info about my user:

```
[ui]
username = User Name <user@gmail.com>
```


### Python setup

- `brew install python` installs `python` and `pip`
- `pip install virtualenv virtualenvwrapper`


#### Python virtualenv

If your virtual environments are broken, then you need to recreate links to the newer version of Python.

Do these two commands *for each* of your project:
```shell
# delete all broken links
find ~/.virtualenvs/my_project_name/ -type l -delete
# create new links to python
virtualenv ~/.virtualenvs/my_project_name/
```


#### Python 3 support

- `brew install python3` installs `python3` and `pip3`
- `pip3 install virtualenv virtualenvwrapper`

To create virtual environment with `python3` support you need to specify path to specific version of python.

```shell
mkvirtualenv --python=$(which python3) project_name
# you can also use my shortcut from ~/.profile (see link to file above)
mkvirtualenv3 project_name
```


#### Django completion

Add autocompletion in terminal when we type `manage.py` or `django-admin.py` and press `<tab>` button two times.

- `cd /usr/local/etc/bash_completion.d/`
- `wget https://raw.github.com/django/django/master/extras/django_bash_completion`
- `source ~/.profile` to affect changes


## Post-installation

- create virtual environments for projects `mkvirtualenv [env_name]` and run `pip install -r requirements.txt`
- restore MySQL/Postgres/MongoDB databases
  - mongodb: `mongodump --out backup/` -> `mongorestore backup/`


## Useful software

This is my list of sofrware that I use:

### Source code editor

I use **Visual Studio Code** and you can read [how to configure VS Code on macOS for Python dev](VSCode.md).

In the past I've used [Sublime Text 3](http://www.sublimetext.com/3) and tried [Atom](ATOM.md).

### Development tools

- [GitHub Desktop](https://desktop.github.com) - GUI for git repos. In the past I also used [SourceTree](http://www.sourcetreeapp.com)
- [MySQL Workbench](http://dev.mysql.com/downloads/workbench/). Also I use [Postico](https://eggerapps.at/postico/) for Postgres
- [Docker](https://docs.docker.com/docker-for-mac/docker-toolbox/)

### Other software

- From **App Store**: Pages, Numbers, Keynote, Pixelmator, Graphic, 1Password, The Unarchiver, Pocket
- [DropBox](https://www.dropbox.com)
- [Skype](http://www.skype.com)
- [Google Chrome](http://www.google.com/chrome)
- [VirtualBox](https://www.virtualbox.org)
- [TunnelBlick](https://code.google.com/p/tunnelblick/) - graphical OpenVPN for Mac
- [Team Viewer](http://www.teamviewer.com/en/index.aspx) - share your screen
- [XMind](http://www.xmind.net) - save your minds in graphical representation
- [VLC Video Player](http://www.videolan.org/vlc/download-macosx.html)


## Login to web services on macOS

- Login to [google.com](http://google.com) and auto-setup macOS to work with: mail, calendar, etc
- Login to [facebook](http://facebook.com), [twitter](http://twitter.com) and [linkedin](http://linkedin.com) and allow auto-setup on macOS


## Read more

- [How To Setup Ubuntu Web Server](https://github.com/1st/setup-web-server)
