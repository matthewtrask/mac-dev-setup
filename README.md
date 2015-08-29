# Mac OS X Dev Setup

This document describes how I set up my developer environment on a new MacBook or iMac. We will set up [Node](http://nodejs.org/), [PHP](http://www.php.net/), [Python](http://www.python.org/), [Ruby](http://www.ruby-lang.org/), and [Go](http://golang.org/) environments.

The document assumes you are new to Mac. The steps below were tested on **OS X Mountain Lion**.


- [System update](#system-update)
- [System preferences](#system-preferences)
- [Google Chrome](#google-chrome)
- [Homebrew](#homebrew)
- [GNU Core Utilities](#gnu-core-utilities)
- [Bash v4](#bash-v4)
- [Bash Completions](#bash-completions)
- [Generic Colouriser](#generic-colouriser)
- [Consolas](#consolas)
- [Beautiful terminal](#beautiful-terminal)
- [iTerm2](#iterm2)
- [Git](#git)
- [Vim](#vim)
- [PHP](#php)
- [Python](#python)
- [IPython](#ipython)
- [Numpy, Scipy, matplotlib, and scikit-learn](#numpy-scipy-matplotlib-and-scikit-learn)
- [pandas](#pandas)
- [Python Virtualenv](#python-virtualenv)
- [R](#r)
- [Node.js](#nodejs)
- [Ruby and RVM](#ruby-and-rvm)
- [Go](#go)
- [Heroku](#heroku)
- [MongoDB](#mongodb)
- [PostgreSQL](#postgresql)
- [Redis](#redis)
- [MySQL](#mysql)
- [VirtualBox](#virtualbox)
- [Vagrant](#vagrant)
- [Docker](#docker)
- [Apps](#apps)
- [Things from fork I dont use personally](#things-from-fork-i-dont-use-personally)
    - [Sublime Text](#sublime-text)

## System update

First thing you need to do, on any OS acutally, is update the system! For that: **Apple Icon > Software Update...**


## System preferences

If this is a new computer, there are a couple tweaks I like to make to the System Preferences. Feel free to follow these, or to ignore them, depending on your personal preferences.

In **Apple Icon > System Preferences**:

- Trackpad > Tap to click
- Keyboard > Key Repeat > Fast (all the way to the right)
- Keyboard > Delay Until Repeat > Short (all the way to the right)
- Dock > Automatically hide and show the Dock


## Google Chrome

Install your favorite browser, mine happens to be Chrome.

Download from [www.google.com/chrome](https://www.google.com/intl/en/chrome/browser/). Open the **.dmg** file once it's done downloading (this will mount the disk image), and drag and drop the **Google Chrome** app into the Applications folder (on the Mac, most applications are installed this way). When done, you can unmount the disk in Finder (the small "eject" icon next to the disk under **Devices**).

You can optionally install [Google Chrome Canary](https://www.google.com/intl/en/chrome/browser/canary.html), which gets the latest updates first, however also has noticable bugs at times.


## Homebrew

Package managers make it so much easier to install and update applications (for Operating Systems) or libraries (for programming languages). The most popular one for OS X is [Homebrew](http://brew.sh).

### Install

An important dependency before Homebrew can work is the **Command Line Tools** for **Xcode**. These include compilers that will allow you to build things from source.

Now, Xcode weights something like 2GB, and you don't need it unless you're developing iPhone or Mac apps. Good news is Apple provides a way to install only the Command Line Tools, without Xcode. To do this you need to go to [http://developer.apple.com/downloads](http://developer.apple.com/downloads), and sign in with your Apple ID (the same one you use for iTunes and app purchases). Unfortunately, you're greeted by a rather annoying questionnaire. All questions are required, so feel free to answer at random.

Once you reach the downloads page, search for "command line tools", and download the latest **Command Line Tools (OS X Mountain Lion) for Xcode**. Open the **.dmg** file once it's done downloading, and double-click on the **.mpkg** installer to launch the installation. When it's done, you can unmount the disk in Finder.

**Note**: If you are running **OS X 10.9 Mavericks**, then you can install the Xcode Command Line Tools directly from the command line with `$ xcode-select --install`, and you don't have to go through the download page and the questionnaire.

Finally, we can install Hombrew! In the terminal paste the following line (without the `$`), hit **Enter**, and follow the steps on the screen:

```bash
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

One thing we need to do is tell the system to use programs installed by Hombrew (in `/usr/local/bin`) rather than the OS default if it exists. We do this by adding `/usr/local/bin` to your `$PATH` environment variable:

```bash
$ echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile
```

Open an new terminal tab with **Cmd+T** (you should also close the old one), then run the following command to make sure everything works:

```bash
$ brew doctor
```

### Usage

To install a package (or **Formula** in Homebrew vocabulary) simply type:

```bash
$ brew install <formula>
```

To update Homebrew's directory of formulae, run:

```bash
$ brew update
```

**Note**: I've seen that command fail sometimes because of a bug. If that ever happens, run the following (when you have Git installed):

```bash
$ cd /usr/local
$ git fetch origin
$ git reset --hard origin/master
```

To see if any of your packages need to be updated:

```bash
$ brew outdated
```

To update a package:

```bash
$ brew upgrade <formula>
```

Homebrew keeps older versions of packages installed, in case you want to roll back. That rarely is necessary, so you can do some cleanup to get rid of those old versions:

```bash
$ brew cleanup
```

To see what you have installed (with their version numbers):

```bash
$ brew list --versions
```

## GNU Core Utilities
The GNU Core Utilities are the basic file, shell and text manipulation utilities of the GNU operating system. These are the core utilities which are expected to exist on every operating system. However the one's that come preinstalled with Mac are a bit older.

```bash
$ brew install coreutils
# Install GNU `find`, `locate`, `updatedb`, and `xargs`, g-prefixed
$ brew install findutils
```


## Bash v4
Do to lack of Associative Arrays in Bash (Version < 3) i decided to install bash from Homebrew.

```bash
$ brew install bash
```

After installation, you must set your new bash as default bash in to your system. Homebrew installs bash to `/usr/local/bin/`

If you wish to check your current bash version, just echo these variables:

```bash
$ echo $BASH_VERSION # gives full version
$ echo $BASH_VERSINFO # gives major version number
```

We will use chsh command to proceed but before that, we must add this new bash location in to `/etc/shells`. Otherwise, system will alert an error. Now, lets edit file:

```bash
$ sudo vim /etc/shells
```

add this line at the end of the list:

    /usr/local/bin/bash

Now, we can run chsh command:

```bash
$ chsh -s /usr/local/bin/bash YOUR_COMPUTERS_NAME # ex. for me this was macinator
```

Enter your password to proceed. Now you can restart Terminal.app and check if the installation is correct:

```bash
$ echo $BASH_VERSION
```

## Bash Completions

All hail the bash completions + `tab`. You can thank me lata!

```bash
$ brew install bash-completion
```

## Generic Colouriser
[Generic Colouriser](http://kassiopeia.juls.savba.sk/~garabik/software/grc/README.txt) is a great utility which can be used for colourising many different types of output and log files.

### Install

```bash
$ brew install grc
```

Then just add the following to your `.bash_profile`:

```bash
source "`brew --prefix grc`/etc/grc.bashrc"
```

## Consolas

I really like the Consolas font for coding. Being a Microsoft (!) font, it is not installed by default. Since we're going to be looking at a lot of terminal output and code, let's install it now.

There are two ways we can install it. If you bought **Microsoft Office for Mac**, install that and Consolas will be installed as well.

If you don't have Office, follow these steps:

```bash
$ brew install cabextract
$ cd ~/Downloads
$ mkdir consolas
$ cd consolas
$ curl -O http://download.microsoft.com/download/f/5/a/f5a3df76-d856-4a61-a6bd-722f52a5be26/PowerPointViewer.exe
$ cabextract PowerPointViewer.exe
$ cabextract ppviewer.cab
$ open CONSOLA*.TTF
```

And click **Install Font**. Thanks to Alexander Zhuravlev for his [post](http://blog.ikato.com/post/15675823000/how-to-install-consolas-font-on-mac-os-x).

## Beautiful terminal

Since we spend so much time in the terminal, we should try to make it a more pleasant and colorful place. What follows might seem like a lot of work, but trust me, it'll make the development experience so much better.

### Add theme
Let's add some color. I'm a big fan of the [Solarized](http://ethanschoonover.com/solarized) color scheme. It is supposed to be scientifically optimal for the eyes. I just find it pretty.

Scroll down the page and download the latest version. Unzip the archive. In it you will find the `osx-terminal.app-colors-solarized` folder with a `README.md` file, but I will just walk you through it here:

- In **Terminal > Preferences**, under **Settings**, cclick the cog at the bottom left to **Import**, find and open the two **.terminal** files we downloaded.
- Go back to **Settings** and select **Solarized Dark** to activate it, hit **Default** to make it the default theme. Voila!

### Change the font

Let's go ahead and change the font. In **Terminal > Preferences...**, under the tab **Settings**, section **Text**, change both fonts to **Consolas 13pt**.

### Customizations

**Note**: You don't have to do this, but there is one color in the **Solarized Dark** preset I don't agree with, which is *Bright Black*. You'll notice it's too close to *Black*. So I change it to be the same as *Bright Yellow*, i.e. **R 83 G 104 B 112**.

Not a lot of colors yet. We need to tweak a little bit our Unix user's profile for that. This is done (on OS X and Linux), in the `~/.bash_profile` text file (`~` stands for the user's home directory).

We'll come back to the details of that later, but for now, just download the files [.bash_profile](/jfrazelle/mac-dev-setup/blob/master/.bash_profile), [.helpers](/jfrazelle/mac-dev-setup/blob/master/.helpers), attached to this document into your home directory (`.bash_profile` is the one that gets loaded, I've set it up to call the others as well.):

```bash
$ cd ~
$ curl -O https://raw.githubusercontent.com/rocketpastsix/mac-dev-setup/master/.bash_profile
$ curl -O https://raw.githubusercontent.com/rocketpastsix/mac-dev-setup/master/.helpers
$ curl -O https://raw2.github.com/mathiasbynens/dotfiles/master/.aliases
$ curl -O https://raw2.github.com/mathiasbynens/dotfiles/master/.bash_prompt
$ curl -O https://raw2.github.com/mathiasbynens/dotfiles/master/.exports
$ curl -O https://raw2.github.com/mathiasbynens/dotfiles/master/.functions
$ curl -O https://raw2.github.com/mathiasbynens/dotfiles/master/.inputrc
```

At this point you can also change your computer's name, which shows up in this terminal prompt. If you want to do so, go to **System Preferences** > **Sharing**. For example, I changed mine from "Jess's MacBook Pro" to just "Jess-MacBook-Pro", so it shows up as `Jess-MacBook-Pro` in the terminal.

Now we have a terminal we can work with!

Thanks to Mathias Bynens for his awesome [dotfiles](https://github.com/mathiasbynens/dotfiles). Also many thanks to Zach Holman's [dotfiles](https://github.com/holman/dotfiles).

### iTerm2

Also just like we did above for terminal, install the [Solarized](http://ethanschoonover.com/solarized) color scheme (this time using `iterm2-colors-solarized` instead of `osx-terminal.app-colors-solarized`).

Since we're going to be spending a lot of time in the command-line, let's install a better terminal than the default one. Download and install [iTerm2](http://www.iterm2.com/) (the newest version, even if it says "beta release").

Or install using Homebrew Cask:

```bash
$ brew tap caskroom/cask
$ brew install brew-cask
$ brew tap caskroom/versions
# to save apps in /Applications
$ export HOMEBREW_CASK_OPTS="--appdir=/Applications"
$ brew cask install iterm2-beta
```

In **Finder**, drag and drop the **iTerm** Application file into the **Applications** folder.

You can now launch iTerm, through the **Launchpad** for instance.

Let's just quickly change some preferences. In **iTerm > Preferences...**, under the tab **General**, uncheck **Confirm closing multiple sessions** and **Confirm "Quit iTerm2 (Cmd+Q)" command** under the section **Closing**.

In the tab **Profiles**, create a new one with the "+" icon, and rename it to your first name for example. Then, select **Other Actions... > Set as Default**. Finally, under the section **Window**, change the size to something better, like **Columns: 90** and **Rows: 40**. Under **General**, change to "Reuse previous session's directory".

When done, hit the red "X" in the upper left (saving is automatic in OS X preference panes). Close the window and open a new one to see the size change.

#### Option-Right & Option-Left
Go to the Keys tab and change **Option Right** to "Send Escape Sequence" **f** & **Option Left** to "Send Escape Sequence" **B**


## Git

What's a developer without [Git](http://git-scm.com/)? To install, simply run:

```bash
$ brew install git
```

When done, to test that it installed fine you can run:

```bash
$ git --version
```

And `$ which git` should output `/usr/local/bin/git`.

Let's set up some basic configuration. Download the [.gitconfig](/mathiasbynens/dotfiles/blob/master/.gitconfig) file to your home directory:

```bash
$ cd ~
$ curl -O https://raw2.github.com/mathiasbynens/dotfiles/master/.gitconfig
```

It will add some color to the `status`, `branch`, and `diff` Git commands, as well as a couple aliases. Feel free to take a look at the contents of the file, and add to it to your liking.

Next, we'll define your Git user (should be the same name and email you use for [GitHub](https://github.com/) and [Heroku](http://www.heroku.com/)):

```bash
$ git config --global user.name "Your Name Here"
$ git config --global user.email "your_email@youremail.com"
```

They will get added to your `.gitconfig` file.

To push code to your GitHub repositories, we're going to use the recommended HTTPS method (versus SSH). So you don't have to type your username and password everytime, let's enable Git password caching as described [here](https://help.github.com/articles/set-up-git):

```bash
$ git config --global credential.helper osxkeychain
```

**Note**: On a Mac, it is important to remember to add `.DS_Store` (a hidden OS X system file that's put in folders) to your `.gitignore` files. You can take a look at this repository's [.gitignore](https://github.com/jfrazelle/mac-dev-setup/blob/master/.gitignore) file for inspiration.

### Make git logs pretty
Based off [this](https://coderwall.com/p/euwpig) article.

Type into terminal:

```bash
$ git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

Running ```git lg``` shows the pretty log and ```git lg -p``` shows the lines that changed.


## Vim

My favorite text-editor is [Vim](http://www.vim.org/). It is a very popular text editor inside the terminal, and is usually pre-installed on any Unix system.

For example, when you run a Git commit, it will open Vim to allow you to type the commit message.

I suggest you read a tutorial on Vim. Grasping the concept of the two "modes" of the editor, **Insert** (by pressing `i`) and **Normal** (by pressing `Esc` to exit Insert mode), will be the part that feels most unatural. After that it's just remembering a few important keys.

### Configuration

Vim's default settings aren't great, and you could spend a lot of time tweaking your configuration (the `.vimrc` file).

I already did all the work for you [here](https://github.com/jfrazelle/.vim).

Install my .vim files by running:

```bash
$ cd ~/
$ git clone --recursive git@github.com:jfrazelle/.vim.git ~/.vim
$ cp ~/.vim/vimrc.txt ~/.vimrc
```

With that, Vim will look a lot better next time you open it!

* If upon firing up vim, you get errors for Pathogen and not being able to find
  Solarized, read [this](https://github.com/altercation/vim-colors-solarized).
  It will clear everything right up.

### Install
You can optionally install a more recent version of vim.

```bash
$ brew install vim --override-system-vi
```


## PHP
OS X, like Linux, ships with [PHP](http://php.net/) already installed. However to run PHP apps locally you will have to make a few tweaks.

Install Latest PHP

```bash
$ brew tap josegonzalez/homebrew-php
$ brew install php55
```

In your ```/etc/apache2/httpd.conf``` file make sure ```LoadModule php5_module libexec/apache2/libphp5.so``` is not commented out.

Next, if you do not currently have a ```~/Sites``` directory, create one. Then make sure you have a file in ```/etc/apache2/users/``` that is named after your computer. For example my computer is named "macinator" so I have a ```macinator.conf``` file that looks like the following:

    <Directory "/Users/macinator/Sites">
        Options Indexes MultiViews FollowSymLinks
        AllowOverride None
        Order allow,deny
        Allow from all
    </Directory>

### Virtual Hosts
Unless you will only ever be working on a single site, you need a way to have multiple sites available. A convenient way is to create local DNS entries and virtual hosts.

First of all you’ll need a way to enter local DNS entries – yoursite.dev, test.local or whatever you prefer. You can add as many entries as you need by editing the ```/etc/hosts``` file:

    127.0.0.1             localhost
    255.255.255.255       broadcasthost
    ::1                   localhost
    fe80::1%lo0           localhost
    127.0.0.1             jess.dev
    127.0.0.1             blog-project.dev

Next create the virtual hosts in ```/etc/apache2/extra/httpd-vhosts.conf```:

    NameVirtualHost *:80
    <VirtualHost *:80>
        ServerName jess.dev
        DocumentRoot "/Volumes/Master/macinator/Sites/"
    </VirtualHost>
    <VirtualHost *:80>
        ServerName blog-project.dev
        DocumentRoot "/Volumes/Master/macinator/Sites/blog-project"
    </VirtualHost>

Restart Apache ```sudo apachectl restart``` and you are good to go.

### Better Directory Theme
I like to swap out the default Apache directory listing with something a bit prettier.

Be sure you have `mod_autoindex` loaded.

Add the contents of directory-theme repo to the root folder of your localhost (ex. Sites)

```bash
$ cd ~/Sites/
$ git clone git@github.com:jfrazelle/directory-theme.git
$ cp -r directory-theme/* .
$ rm -rf directory-theme/
$ mv htaccess-txt.txt .htaccess
```

 Now when viewing your sites folder via browser it should have a much prettier theme. (this is if your sites folder is viewed via it's virtual host url, see above for virtual hosts)

## Python

OS X, like Linux, ships with [Python](http://python.org/) already installed. But you don't want to mess with the system Python (some system tools rely on it, etc.), so we'll install our own version with Homebrew. It will also allow us to get the very latest version of Python 2.7.

The following command will install Python 2.7 and any dependencies required (it can take a few minutes to build everything):

```bash
$ brew install python
```

When finished, you should get a summary in the terminal. Running `$ which python` should output `/usr/local/bin/python`.

It also installed [Pip]() (and its dependency [Distribute]()), which is the package manager for Python. Let's upgrade them both:

```bash
$ pip install --upgrade pip
```

Executable scripts from Python packages you install will be put in `/usr/local/bin`.

### Pip Usage

Here are a couple Pip commands to get you started. To install a Python package:

```bash
$ pip install <package>
```

To upgrade a package:

```bash
$ pip install --upgrade <package>
```

To see what's installed:

```bash
$ pip freeze
```

To uninstall a package:

```bash
$ pip uninstall <package>
```


## IPython

[IPython](http://ipython.org/) is an awesome project which provides a much better Python shell than the one you get from running `$ python` in the command-line. It has many cool functions (running Unix commands from the Python shell, easy copy & paste, creating Matplotlib charts in-line, etc.) and I'll let you refer to the [documentation](http://ipython.org/ipython-doc/stable/index.html) to discover them.

### Install

Before we install IPython, we'll need to get some dependencies. Run the following:

```bash
$ brew update # Always good to do
$ brew install zeromq # Necessary for pyzmq
$ brew install pyqt # Necessary for the qtconsole
```

It may take a few minutes to build these.

Once it's done, we can install IPython with all the available options:

```bash
$ pip install ipython[zmq,qtconsole,notebook,test]
```

### Usage

You can launch IPython from the command line with `$ ipython`, but what's more interesting is to use its [QT Console](http://ipython.org/ipython-doc/stable/interactive/qtconsole.html). Launch the QT Console by running:

```bash
$ ipython qtconsole
```

You can also customize the font it uses:

```bash
$ ipython qtconsole --ConsoleWidget.font_family="Consolas" --ConsoleWidget.font_size=13
```

And since I'm lazy and I don't want to type or copy & paste that all the time, I'm going to create an alias for it. Create a `.extra` text file in your home directory with `$ subl ~/.extra` (I've set up `.bash_profile` to load `.extra`), and add the following line:

```bash
alias ipy='ipython qtconsole --ConsoleWidget.font_family="Consolas" --ConsoleWidget.font_size=13'
```

Open a fresh terminal. Now when you run `$ ipy`, it will launch the QT Console with your configured options.

To use the in-line Matplotlib functionality (nice for scientific computing), run:

```bash
$ ipy --pylab=inline
```

To be able to run inline videos install (this takes about 2 minutes to install):

```bash
$ brew install ffmpeg
```

If you are getting an error message when running iPython with the following:
> Python History requires SQLite, your history will not be saved.

.. and you know you have sqlite installed, run `brew rm sqlite python` then `brew install python` and the error will be fixed.

## Numpy, Scipy, matplotlib, and scikit-learn

[Numpy](http://numpy.scipy.org/), [Scipy](http://www.scipy.org/SciPy), [matplotlib](http://matplotlib.org/), and [scikit-learn](http://scikit-learn.org/stable/) are scientific libraries for Python and are always a little tricky to install from source because they have all these dependencies they need to build correctly. Luckily for us, [Samuel John](http://www.samueljohn.de/) has put together some [Homebrew formulae](https://github.com/samueljohn/homebrew-python) to make it easier to install these Python libraries.

Install the `gfortran` dependency, part of `gcc`, which we will need to build the libraries (this takes about 5 minutes to install):

```bash
$ brew install gcc
```

You can install Numpy with:

```bash
$ pip install numpy
```

Test your Numpy installation:

```bash
$ python
```
```python
import numpy
print numpy.__version__
print numpy.__file__
quit()
```

You can install Scipy with:

```bash
$ pip install scipy
```

Test your Scipy installation:

```bash
$ python
```
```python
import scipy
print scipy.__version__
print scipy.__file__
quit()
```

Then install matplotlib

```bash
$ pip install matplotlib
```

(All three of these may take a few minutes to download.)
After installing matplotlib you may get an error, `* The following required packages can not be built: * freetype`, if you do, you can resolve it by installing the `freetype` dependency:

```bash
$ brew install freetype
```

Then try installing matplotlib again:

```bash
$ pip install matplotlib
```

Then install scikit-learn:

```bash
$ pip install -U scikit-learn
```

### pandas

[pandas](http://pandas.pydata.org/) is an open source, BSD-licensed library providing high-performance, easy-to-use data structures and data analysis tools for the Python programming language.

#### Install

```bash
$ pip install pandas
```

#### pandasjson Install

Easily convert to and from JSON for use with pandas.


```bash
$ git clone https://github.com/pydata/pandasjson
$ cd pandasjson
$ pip install .
$ cd ../
$ rm -rf pandasjson
```


### Python Virtualenv

[Virtualenv](http://www.virtualenv.org/) is a tool that creates an isolated Python environment for each of your projects. For a particular project, instead of installing required packages globally, it is best to install them in an isolated folder in the project (say a folder named `venv`), that will be managed by virtualenv.

The advantage is that different projects might require different versions of packages, and it would be hard to manage that if you install packages globally. It also allows you to keep your global `/usr/local/lib/python2.7/site-packages` folder clean, containing only critical or big packages that you always need (like IPython, Numpy).

#### Install

To install virtualenv, simply run:

```bash
$ pip install virtualenv
```

#### Usage

Let's say you have a project in a directory called `myproject`. To set up virtualenv for that project:

```bash
$ cd myproject/
$ virtualenv venv --distribute
```

If you want your virtualenv to also inherit globally installed packages (like IPython or Numpy mentioned above), use:

```bash
$ virtualenv venv --system-site-packages
```

These commands create a `venv` subdirectory in your project where everything is installed. You need to **activate** it first though (in every terminal where you are working on your project):

```bash
$ source venv/bin/activate
```

You should see a `(venv)` appear at the beginning of your terminal prompt indicating that you are working inside the virtualenv. Now when you install something:

```bash
$ pip install <package>
```

It will get installed in the `venv` folder, and not conflict with other projects.

**Important**: Remember to add `venv` to your project's `.gitignore` file so you don't include all of that in your source code!

As mentioned earlier, I like to install big packages (like Numpy), or packages I always use (like IPython) globally. All the rest I install in a virtualenv.

You can create two aliases in your `.bash_profile` with the following:

```bash
alias pyvirall='virtualenv venv --system-site-packages && source venv/bin/activate'
alias pyvir='virtualenv venv && source venv/bin/activate'
```


## R

R is a software environment for statistical computing and graphics.

First install [XQuartz](https://xquartz.macosforge.org/landing/) <-- click the link or use Homebrew Cask:

```bash
$ brew tap caskroom/cask
$ brew install brew-cask
$ brew cask install xquartz
```

This relies on you tapping ```brew tap homebrew/science``` and ```brew install gfortran``` from above.

Then, install r (this takes about 7 minutes):

```bash
$ brew install r
```

To test your installation:

```bash
$ r
```r
x <- 4+5
x
# [1] 9
addup <- function(a, b=10)
{
return (a+b)
}
addup(4,5)
# [1] 9
```

When you're done, quit the R console:

```r
q()
```

You can now install whatever R packages you want. For those interested, [here’s a list of well known and commonly used packages](https://gist.github.com/hernamesbarbara/9141258) to jumpstart your collection.


## Node.js

Install [Node.js](http://nodejs.org/) with Homebrew:

```bash
$ brew update
$ brew install node
```

The formula also installs the [npm](https://npmjs.org/) package manager. However, as suggested by the Homebrew output, we need to add `/usr/local/share/npm/bin` to our path so that npm-installed modules with executables will have them picked up.

To do so, add this line to your `~/.bash_profile` file, before the `export PATH` line:

```bash
PATH=/usr/local/share/npm/bin:$PATH
```

Open a new terminal for the `$PATH` changes to take effect.

**NOTE: may not be necessary** We also need to tell npm where to find the Xcode Command Line Tools, by running:

```bash
$ sudo xcode-select -switch /usr/bin
```

Node modules are installed locally in the `node_modules` folder of each project by default, but there are at least two that are worth installing globally. Those are [Nodemon](https://github.com/remy/nodemon) and [Grunt](http://gruntjs.com/):

```bash
$ npm install -g nodemon
$ npm install -g grunt-cli
```

### Npm usage

To install a package:

```bash
$ npm install <package> # Install locally
$ npm install -g <package> # Install globally
```

To install a package and save it in your project's `package.json` file:

```bash
$ npm install <package> --save
```

To see what's installed:

```bash
$ npm list # Local
$ npm list -g # Global
```

To find outdated packages (locally or globally):

```bash
$ npm outdated [-g]
```

To upgrade all or a particular package:

```bash
$ npm update [<package>]
```

To uninstall a package:

```bash
$ npm uninstall <package>
```

## Ruby and RVM

Like Python, [Ruby](http://www.ruby-lang.org/) is already installed on Unix systems. But we don't want to mess around with that installation. More importantly, we want to be able to use the latest version of Ruby.

### Install

When installing Ruby, best practice is to use [RVM](https://rvm.io/) (Ruby Version Manager) which allows you to manage multiple versions of Ruby on the same machine. Installing RVM, as well as the latest version of Ruby, is very easy. Just run:

```bash
$ curl -L https://get.rvm.io | bash -s stable --ruby
```

When it is done, both RVM and a fresh version of Ruby 2.0 are installed. The following line was also automatically added to your `.bash_profile`:

```bash
[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" # Load RVM into a shell session *as a function*
```

I prefer to move that line to the `.extra` file, keeping my `.bash_profile` clean. I suggest you do the same.

After that, start a new terminal and run:

```bash
$ type rvm | head -1
```

You should get the output `rvm is a function`.

### Usage

The following command will show you which versions of Ruby you have installed:

```bash
$ rvm list
```

The one that was just installed, Ruby 2.0, should be set as default. When managing multiple versions, you switch between them with:

```bash
$ rvm use system # Switch back to system install (1.8)
$ rvm use 2.0.0 --default # Switch to 2.0.0 and sets it as default
```

Run the following to make sure the version you want is being used (in our case, the just-installed Ruby 1.9.3):

```bash
$ which ruby
$ ruby --version
```

You can install another version with:

```bash
$ rvm install 1.9.3
```

To update RVM itself, use:

```bash
$ rvm get stable
```

[RubyGems](http://rubygems.org/), the Ruby package manager, was also installed:

```bash
$ which gem
```

Update to its latest version with:

```bash
$ gem update --system
```

To install a "gem" (Ruby package), run:

```bash
$ gem install <gemname>
```

To install without generating the documentation for each gem (faster):

```bash
$ gem install <gemname> --no-document
```

To see what gems you have installed:

```bash
$ gem list
```

To check if any installed gems are outdated:

```bash
$ gem outdated
```

To update all gems or a particular gem:

```bash
$ gem update [<gemname>]
```

RubyGems keeps old versions of gems, so feel free to do come cleaning after updating:

```bash
$ gem cleanup
```


## Go
[Go](http://golang.org/) is an open source programming language that makes it easy to build simple, reliable, and efficient software.

### Install
**First**, create the `.go` directory.

```bash
$ mkdir ~/.go
```

Then, add the following to your path, in either your `.path` file or `.bash_profile` file.

```bash
# go path
export GOPATH=$HOME/.go
export PATH=$PATH:$GOPATH/bin
```

Then, installing it is very easy through Homebrew, but first you need Mercurial:

```bash
$ brew install go
```

### Go Tour
To the run the go tour, just run the following:

```bash
$ go get code.google.com/p/go-tour/gotour
$ gotour
```

## Heroku

[Heroku](http://www.heroku.com/), if you're not already familiar with it, is a [Platform-as-a-Service](http://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) that makes it really easy to deploy your apps online. There are other similar solutions out there, but Heroku was among the first and is currently the most popular. Not only does it make a developer's life easier, but I find that having Heroku deployment in mind when building an app forces you to follow modern app development [best practices](http://www.12factor.net/).

### Install

Assuming that you have an account (sign up if you don't), let's install the [Heroku Client](https://devcenter.heroku.com/articles/using-the-cli) for the command-line. Heroku offers a Mac OS X installer, the [Heroku Toolbelt](https://toolbelt.heroku.com/), that includes the client. But for these kind of tools, I prefer using Homebrew. It allows us to keep better track of what we have installed. Luckily for us, Homebrew includes a `heroku-toolbelt` formula:

```bash
$ brew install heroku-toolbelt
```

The formula might not have the latest version of the Heroku Client, which is updated pretty often. Let's update it now:

```bash
$ heroku update
```

Don't be afraid to run `heroku update` every now and then to always have the most recent version.

### Usage

Login to your Heroku account using your email and password:

```bash
$ heroku login
```

If this is a new account, and since you don't already have a public **SSH key** in your `~/.ssh` directory, it will offer to create one for you. Say yes! It will also upload the key to your Heroku account, which will allow you to deploy apps from this computer.

If it didn't offer create the SSH key for you (i.e. your Heroku account already has SSH keys associated with it), you can do so manually by running:

```bash
$ mkdir ~/.ssh
$ ssh-keygen -t rsa
```

Keep the default file name and skip the passphrase by just hitting Enter both times. Then, add the key to your Heroku account:

```bash
$ heroku keys:add
```

Once the key business is done, you're ready to deploy apps! Heroku has a great [Getting Started](https://devcenter.heroku.com/articles/python) guide, so I'll let you refer to that (the one linked here is for Python, but there is one for every popular language). Heroku uses Git to push code for deployment, so make sure your app is under Git version control. A quick cheat sheet (if you've used Heroku before):

```bash
$ cd myapp/
$ heroku create myapp
$ git push heroku master
$ heroku ps
$ heroku logs -t
```

The [Heroku Dev Center](https://devcenter.heroku.com/) is full of great resources, so be sure to check it out!

## MongoDB

[MongoDB](http://www.mongodb.org/) is a popular [NoSQL](http://en.wikipedia.org/wiki/NoSQL) database.

### Install

Installing it is very easy through Homebrew:

```bash
$ brew update
$ brew install mongo
```

### Usage

In a terminal, start the MongoDB server:

```bash
$ mongod
```

In another terminal, connect to the database with the Mongo shell using:

```bash
$ mongo
```

I'll let you refer to MongoDB's [Getting Started](http://docs.mongodb.org/manual/tutorial/getting-started/) guide for more!

## PostgreSQL

[PostgreSQL](http://www.postgresql.org/) is a powerful, open source object-relational database system.

### Install

To install PostgreSQL, use Homebrew:

```bash
$ brew update
$ brew install postgresql
```

### Create/Upgrade a database
If this is your first time installing Postgres with Homebrew, you’ll need to create a database with:

```bash
$ initdb /usr/local/var/postgres -E utf8
```

### Usage

Start a local PostgreSQL server using the default configuration settings with:

```bash
$ pg_ctl -D /usr/local/var/postgres -l /usr/local/var/postgres/server.log start
```

Stop the PostgreSQL server:

```bash
$ pg_ctl -D /usr/local/var/postgres stop -s -m fast
```

Or you can create two aliases in your `.bash_profile` with the following:

```bash
alias pgdown='pg_ctl -D /usr/local/var/postgres stop -s -m fast'
alias pgup='pg_ctl -D /usr/local/var/postgres -l /usr/local/var/postgres/server.log start'
```

You can also add a `.psqlrc` in your root with the following to auto size tables and colorize in the postgres shell:

```bash
\x auto
\set PROMPT1 '%[%033[1;32;40m%]%M:%&gt; %n@%/%[%033[0m%]% # '
```

## Redis

[Redis](http://redis.io/) is a blazing fast, in-memory, key-value store, that uses the disk for persistence. It's kind of like a NoSQL database, but there are a lot of [cool things](http://oldblog.antirez.com/post/take-advantage-of-redis-adding-it-to-your-stack.html) that you can do with it that would be hard or inefficient with other database solutions. For example, it's often used as session management or caching by web apps, but it has many other uses.

### Install

To install Redis, use Homebrew:

```bash
$ brew update
$ brew install redis
```

### Usage

Start a local Redis server using the default configuration settings with:

```bash
$ redis-server
```

For advanced usage, you can tweak the configuration file at `/usr/local/etc/redis.conf` (I suggest making a backup first), and use those settings with:

```bash
$ redis-server /usr/local/etc/redis.conf
```

In another terminal, connect to the server with the Redis command-line interface using:

```bash
$ redis-cli
```

I'll let you refer to Redis' [documentation](http://redis.io/documentation) or other tutorials for more information.

## MySQL

### Install

We will install [MySQL](http://www.mysql.com/) using Homebrew, which will also install some header files needed for MySQL bindings in different programming languages (MySQL-Python for one).

To install, run:

```bash
$ brew update # Always good to do
$ brew install mysql
```

As you can see in the ouput from Homebrew, before we can use MySQL we first need to set it up with:

```bash
$ unset TMPDIR
$ mkdir /usr/local/var
$ mysql_install_db --verbose --user=`whoami` --basedir="$(brew --prefix mysql)" --datadir=/usr/local/var/mysql --tmpdir=/tmp
```

### Usage

To start the MySQL server, use the `mysql.server` tool:

```bash
$ mysql.server start
```

To stop it when you are done, run:

```bash
$ mysql.server stop
```

You can see the different commands available for `mysql.server` with:

```bash
$ mysql.server --help
```

To connect with the command-line client, run:

```bash
$ mysql -uroot
```

(Use `exit` to quit the MySQL shell.)

**Note**: By default, the MySQL user `root` has no password. It doesn't really matter for a local development database. If you wish to change it though, you can use `$ mysqladmin -u root password 'new-password'`.


## VirtualBox

[VirtualBox](https://www.virtualbox.org/) is a general-purpose full virtualizer for x86 hardware, targeted at server, desktop and embedded use.

### Install

To install VirtualBox, use Homebrew Cask:

```bash
$ brew tap phinze/homebrew-cask
$ brew install brew-cask
$ brew cask install virtualbox
```


## Vagrant

[Vagrant](http://www.vagrantup.com/) is a tool for building complete development environments. With an easy-to-use workflow and focus on automation, Vagrant lowers development environment setup time, increases development/production parity, and makes the "works on my machine" excuse a relic of the past.

### Install

The easiest way to install Vagrant is to tap Homebrew Cask, from above with VirtualBox, then:

```bash
$ brew cask install vagrant
```

### Vagrant Completions
Add autocomplete for Vagrant to bash completion.

```bash
$ brew tap homebrew/completions
$ brew install vagrant-completion
```

Then just add the following to your `.bash_profile` to source the completions:

```bash
[ -f `brew --prefix`/etc/bash_completion.d/vagrant ]; source `brew --prefix`/etc/bash_completion.d/vagrant
```

## Docker

[Docker](https://www.docker.io/) is an open-source project to easily create lightweight, portable, self-sufficient containers from any application. The same container that a developer builds and tests on a laptop can run at scale, in production, on VMs, bare metal, OpenStack clusters, public clouds and more.

### Install

```bash
$ brew update
$ brew install docker
$ brew install boot2docker
```

### How to use
boot2docker comes with a simple init script that leverage's VirtualBox's `VBoxManage`. You can start, stop and delete the VM right from the command line.

Initialize

```bash
$ boot2docker init
```

Start vm

```bash
$ boot2docker up
```

SSH into vm

```bash
$ boot2docker ssh
```

boot2docker auto logs in, but if you want to SSH into the machine, the credentials are:

```
user: docker
pass: tcuser
```


## Apps

Here is a quick list of some apps I use, and that you might find useful as well:

- [Dropbox](https://www.dropbox.com/): File syncing to the cloud. I put all my documents in Dropbox. It syncs them to all my devices (laptop, mobile, tablet), and serves as a backup as well! **(Free for 2GB)**
- [Google Drive](https://drive.google.com/): File syncing to the cloud too! I use Google Docs a lot to collaborate with others (edit a document with multiple people in real-time!), and sometimes upload other non-Google documents (pictures, etc.), so the app comes in handy for that. **(Free for 5GB)**
- [Alfred](http://www.alfredapp.com/): Alfred saves you time when you search for files online or on your Mac. Be more productive with hotkeys, keywords and file actions at your fingertips. **($17)**
- [ColorSnapper](http://colorsnapper.com/): An easy-to-use tool for quickly finding out the color of any pixel on the screen. It is activated via a system-wide hotkey, giving you a magnifying loupe to easily pick the pixel you need. The resulting color is copied to clipboard in a format of your preference. **($4.99)**


## Things from fork I dont use personally

### Sublime Text

With the terminal, the text editor is a developer's most important tool. Everyone has their preferences, but unless you're a hardcore [Vim](http://en.wikipedia.org/wiki/Vim_(text_editor)) user, a lot of people are going to tell you that [Sublime Text](http://www.sublimetext.com/) is currently the best one out there.

Go ahead and [download](http://www.sublimetext.com/) it. Open the **.dmg** file, drag-and-drop in the **Applications** folder, you know the drill now. Launch the application.

**Note**: At this point I'm going to create a shorcut on the OS X Dock for both for Sublime Text and iTerm. To do so, right-click on the running application and select **Options > Keep in Dock**.

Sublime Text is not free, but I think it has an unlimited "evaluation period". Anyhow, we're going to be using it so much that even the seemingly expensive $60 price tag is worth every penny. If you can afford it, I suggest you [support](http://www.sublimetext.com/buy) this awesome tool. :)

Just like the terminal, let's configure our editor a little. Go to **Sublime Text 2 > Preferences > Settings - User** and paste the following in the file that just opened:

```json
{
    "font_face": "Consolas",
    "font_size": 13,
    "rulers":
    [
        79
    ],
    "highlight_line": true,
    "bold_folder_labels": true,
    "highlight_modified_tabs": true,
    "tab_size": 2,
    "translate_tabs_to_spaces": true,
    "word_wrap": false,
    "indent_to_bracket": true
}
```

Feel free to tweak these to your preference. When done, save the file and close it.

I use tab size 2 for everything except Python and Markdown files, where I use tab size 4. If you have a Python and Markdown file handy (or create dummy ones with `$ touch dummy.py`), for each one, open it and go to **Sublime Text 2 > Preferences > Settings - More > Syntax Specific - User** to paste in:

```json
{
    "tab_size": 4
}
```

Now for the color. I'm going to change two things: the **Theme** (which is how the tabs, the file explorer on the left, etc. look) and the **Color Scheme** (the colors of the code). Again, feel free to pick different ones, or stick with the default.

A popular Theme is the [Soda Theme](https://github.com/buymeasoda/soda-theme). To install it, run:

    $ cd ~/Library/Application\ Support/Sublime\ Text\ 2/Packages/
    $ git clone https://github.com/buymeasoda/soda-theme/ "Theme - Soda"

Then go to **Sublime Text 2 > Preferences > Settings - User** and add the following two lines:

    "theme": "Soda Dark.sublime-theme",
    "soda_classic_tabs": true

Restart Sublime Text for all changes to take affect (Note: on the Mac, closing all windows doesn't close the application, you need to hit **Cmd+Q**).

The Soda Theme page also offers some [extra color schemes](https://github.com/buymeasoda/soda-theme#syntax-highlighting-colour-schemes) you can download and try. But to be consistent with my terminal, I like to use the **Solarized** Color Scheme, which already ships with Sublime Text. To use it, just go to **Sublime Text 2 > Preferences > Color Scheme > Solarized (Dark)**. Again, this is really according to personal flavors, so pick what you want.

Sublime Text 2 already supports syntax highlighting for a lot of languages. I'm going to install a couple that are missing:

    $ cd ~/Library/Application\ Support/Sublime\ Text\ 2/Packages/
    $ git clone https://github.com/jashkenas/coffee-script-tmbundle CoffeeScript
    $ git clone https://github.com/miksago/jade-tmbundle Jade
    $ git clone https://github.com/danro/LESS-sublime.git LESS
    $ git clone -b SublimeText2 https://github.com/kuroir/SCSS.tmbundle.git SCSS
    $ git clone https://github.com/nrw/sublime-text-handlebars Handlebars

Let's create a shortcut so we can launch Sublime Text from the command-line:

    $ cd ~
    $ mkdir bin
    $ ln -s "/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl" ~/bin/subl

Now I can open a file with `$ subl myfile.py` or start a new project in the current directory with `$ subl .`. Pretty cool.

Sublime Text is very extensible. For now we'll leave it like that, we already have a solid installation. To add more in the future, a good place to start would be to install the [Sublime Package Control](http://wbond.net/sublime_packages/package_control/installation).


[![Analytics](https://ga-beacon.appspot.com/UA-29404280-16/mac-dev-setup/README.md)](https://github.com/jfrazelle/mac-dev-setup)
