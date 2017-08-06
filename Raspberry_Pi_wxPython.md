These are the build and install instructions. **READ THEM ALL FIRST!**
Especially the note at the end.

The first part of this is optional. I have tested this on both Python
3.4 (the default Pi install) and on Python 3.6.2. To use Python 3.6 you
need to install it first, which mean building it. If you wish, update
the version numbers to the latest release. I know that this version
works, and it's the most recent as of the writing of these directions.

These instructions are based on the Github gist:

[*https://gist.github.com/dschep/24aa61672a2092246eaca2824400d37f*](https://gist.github.com/dschep/24aa61672a2092246eaca2824400d37f)

Optional:

> $ sudo apt-get update
>
> $ sudo apt-get install build-essential tk-dev libncurses5-dev
> libncursesw5-dev libreadline6-dev libdb5.3-dev libgdbm-dev
> libsqlite3-dev libssl-dev libbz2-dev libexpat1-dev liblzma-dev
> zlib1g-dev

Then download and build Python.

> $ wget https://www.python.org/ftp/python/3.6.2/Python-3.6.2.tar.xz
>
> $ tar xf Python-3.6.2.tar.xz
>
> $ cd Python-3.6.2
>
> $ ./configure –enable-optimizations
>
> $ make
>
> $ sudo make altinstall

Okay so you want or need wxPython 4.0.x on your Raspberry Pi or you like
to watch lots of messages scroll by on long builds. Either way this is
how to do it.

First things first MAKE A VIRTUAL ENVIORNMENT for the build and install.
Okay this isn't strictly needed but if you don't know about venv or
virtual environments, they do keep the environment cleaner for each
project. The only issue is that you need to run the pip install for each
virtual environment you want to use it in. It's your choice.

These instructions will use Python 3.4 but they are identical for 3.6,
just substitute the version number you want. For example:

> $ python3.4 ...

would be

> $ python3.6 ...

Not too scary, right?

These instructions are based on the Github Phoenix README:

[*https://github.com/wxWidgets/Phoenix/blob/master/README.rst*](https://github.com/wxWidgets/Phoenix/blob/master/README.rst)

Okay now to make the virtual environment. I made mine right off the
/home/pi directory but you can put it anywhere. Some like to put all
there virtual environments (virtenv) in specific locations.

Lets make one (wx is the name of the virtenv we are creating, change it
to suit):

> $ cd \~
>
> $ python3.4 -m venv wx
>
> $ source \~/wx/bin/activate

The last line activates the environment. Your prompt should change to
show that you are in an active virtenv. To deactivate type deactivate.
If you log out, close the terminal, or restart the Pi, or open a new
terminal, you need to run the activate command again. If not you won't
be in the virtual environment.

> If your lazy like most programmers. Check out
> [*https://direnv.net/*](https://direnv.net/) and
> [*https://github.com/direnv/direnv/wiki/Python*](https://github.com/direnv/direnv/wiki/Python)
> with some fussing the virtenv will load automagically when you enter a
> directory.

First thing you need is wxPython. Go to:

[*https://pypi.python.org/pypi/wxPython/*](https://pypi.python.org/pypi/wxPython/)
or
[*https://pypi.python.org/pypi/wxPython/4.0.0b1*](https://pypi.python.org/pypi/wxPython/4.0.0b1)
The first link will give you a choice of releases, as before I tested
4.0.0b1and it works, but you might get here later and a newer release is
available. PLEASE use the tarball from these links, I too wanted the
latest, greatest version. Don't. If you download it from github you need
to do a massive amount of work. Let the marvelous people who developed
this package do that, then thank them.

Down at the bottom of the choices you'll see “wxPython-4.0.0b1.tar.gz …
Source”.

Download wxPython-4.0.0b1.tar.gz

Use you browser if you can. Theas the link currently is:

[*https://pypi.python.org/packages/be/b5/fc263904687769cb1db2801fb2899f461bd6a7d65f729455cd378456ac41/wxPython-4.0.0b1.tar.gz\#md5=83bfed89a46b489a4a93437199e6e598*](https://pypi.python.org/packages/be/b5/fc263904687769cb1db2801fb2899f461bd6a7d65f729455cd378456ac41/wxPython-4.0.0b1.tar.gz#md5=83bfed89a46b489a4a93437199e6e598)

Ick.

> $ cd \~
>
> $ mv \~/Downloads/wxPython-4.0.0b1.tar.gz .
>
> $ tar xfz wxPython-4.0.0b1.tar.gz

Okay here we go.

> $ sudo apt-get update
>
> $ sudo apt-get install dpkg-dev build-essential libwebkitgtk-dev
> libjpeg-dev libtiff-dev libgtk2.0-dev libsdl1.2-dev
> libgstreamer-plugins-base0.10-dev libnotify-dev freeglut3
> freeglut3-dev

If you are using Python 3.6 you are all set but if you are using the
pre-installed Python 3:

> $ sudo apt-get install python3.4-dev

Next step, make sure you are in the environment you want to install
wxPython into.

> $ pip3 install -r requirements.txt

Okay the next part is the big one. This will take a while, anywhere from
a few hours, to 12+ hours on a Pi zero.

> $ python3 build.py build

Now to install it in Python as a package:

> $ cd \~
>
> $ pip3 install \~/wxPython-4.0.0b1

Now let’s test it:

> $ cd \~/wxPython-4.0.0b1/demo
>
> $ python3 widgetTest.py

The build.py script has many options, but I will warn you unless you
know what your doing, don't play with them. I had built the package for
ver 3.4 then decided to try 3.6. So I ran the cleanall option to clean
out the last builds binaries. It did and it cleaned all the SIP and
Doxygen bits out too. That defeated the whole point of me getting the
pipy tarball. To clean up, delete the directory and extract it again.

**Other things to note.** There were a few times that my pi seemed to
freeze. Leave it alone for awhile. Give it 15-20 minutes. If it doesn't
recover unplug it and enable the virtenv and restart by using you last
command. Usually the 'pip install'. Above all don't panic.
