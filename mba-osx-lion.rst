====================
Macbook Air v3 Setup
====================

Create a `.bashrc` file
========================

.. parsed-literal::

	# Colors for the pretty
	export CLICOLOR=1
	export LSCOLORS=GxFxCxDxBxegedabagaced

	# Compiler options recommended by various people
	export ARCHFLAGS="-arch x86_64"
	export CC=/usr/bin/gcc-4.2
	export CCFLAGS='-arch i386 -arch x86_64 -pipe'
	export CFLAGS='-arch i386 -arch x86_64 -pipe -no-cpp-precomp'
	export CXXFLAGS='-arch i386 -arch x86_64 -pipe'
	export LDFLAGS='-arch i386 -arch x86_64 -bind_at_load'

	# easy command for nixing .pyc files
	alias rmpyc='find . -type f -name "*.pyc" -print0 | xargs -0 rm -v'	

Get a `real` GCC installer
==========================

Screw XCode. I want my hard drive for my stuff. So I went here:

 * https://github.com/kennethreitz/osx-gcc-installer

I picked the GCC compiler for me and installed it.

Got me a text editor
====================

I've used Textmates off and on since Spring of 2006. Unfortunately it is dated and fundamentally unsupported. So I switched to Sublime 2, which has rough edges but is advancing quickly:

 * http://www.sublimetext.com

I use Sublime bareback - which means I have no extensions.

Yeah, I could use emacs or vi, but I've learned the hard way that just because you can use one of those tools doesn't mean you are any good at coding.

Get me some Homebrew
====================

Macports is dangerous and ugly. Go with homebrew:

 * http://mxcl.github.com/homebrew/

Installation is trivial:

.. parsed-literal::

	$ /usr/bin/ruby -e "$(curl -fsSL https://raw.github.com/gist/323731)"

.. warning:: Some people really don't like it and these are people who when they have problems with a tool, I listen. That said, these are the kind of people who dig into the guts of C code, write their own 0mq based HTTP servers, and play guitar. I'm sure they are doing things with their OSX that are not the normal sort of thing I do.

Then I install wget because I like it:

.. parsed-literal::

	$ brew install wget
	

Python Environment Controls
============================

These are the steps I use to get my environment going. For now, just my system Python but later I'll be doing this on other Python versions:

.. parsed-literal::

	$ easy_install pip
	$ pip install virtualenv
	$ pip install virtualenvwrapper

In my `.bashrc` file I add::

	source /usr/local/bin/virtualenvwrapper.sh

Install Python Imaging Library
==============================

Oddly enough, PIL is not part of the standard library but ElementTree is. And PIL always causes me trouble in virtualenvs or buildouts so I install it in my system Python just in case::

	$ brew install jpeg
	$ pip install PIL

The first command gets the jpeg decoder into your system, the second installs PIL. 

Install LXML
============

Like PIL, I've had grief with LXML in the past with all it's dependencies. Can't we just get this into core Python? Probably not because I think some things are super dependant on things that would require cygwin on Windows. So...::

	$ pip install lxml

Fixing the postgresql initdb
==============================

.. parsed-literal::

	$ sudo sysctl -w kern.sysv.shmall=65536
	$ sudo sysctl -w kern.sysv.shmmax=16777216
	$ brew install postgresql
	$ initdb /usr/local/var/postgres
	$ postgres -D /usr/local/var/postgres
	
My current .bashrc file
=======================

.. parsed-literal::

# pygments and docutils stuff
export PATH=/usr/local/bin:/usr/local/bin/rst2html.py:$PATH
export CLICOLOR=1
export LSCOLORS=GxFxCxDxBxegedabagaced
export TM_RST2HTML=/usr/local/bin/rst2html.py

# Compilier options
export ARCHFLAGS="-arch x86_64"
export CC=/usr/bin/gcc-4.2
export CCFLAGS='-arch i386 -arch x86_64 -pipe'
export CFLAGS='-arch i386 -arch x86_64 -pipe -no-cpp-precomp'
export CXXFLAGS='-arch i386 -arch x86_64 -pipe'
export LDFLAGS='-arch i386 -arch x86_64 -bind_at_load'

source /usr/local/bin/virtualenvwrapper.sh

alias rmpyc='find . -type f -name "*.pyc" -print0 | xargs -0 rm -v'


