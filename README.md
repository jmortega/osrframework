	================================================================
	OSRFramework  Copyright (C) 2015  F. Brezo and Y. Rubio, i3visio
	================================================================

[![Version in PyPI](https://img.shields.io/pypi/v/osrframework.svg)]()
[![Downloads/Month in PyPI](https://img.shields.io/pypi/dm/osrframework.svg)]()
[![License](https://img.shields.io/badge/license-GNU%20General%20Public%20License%20Version%203%20or%20Later-blue.svg)]()

Description:
============
OSRFramework is a GPLv3+ set of libraries developed by i3visio to perform Open Source
Intelligence tasks. They include references to a bunch of different applications 
related to username checking, information leaks research, deep web search, regular
expressions extraction and many others. At the same time, by means of ad-hoc Maltego 
transforms, OSRFramework provides a way of making these queries graphically.


License: GPLv3+
===============

This is free software, and you are welcome to redistribute it under certain conditions.

	This program is free software: you can redistribute it and/or modify
	it under the terms of the GNU General Public License as published by
	the Free Software Foundation, either version 3 of the License, or
	(at your option) any later version.

	This program is distributed in the hope that it will be useful,
	but WITHOUT ANY WARRANTY; without even the implied warranty of
	MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
	GNU General Public License for more details.

	You should have received a copy of the GNU General Public License
	along with this program.  If not, see <http://www.gnu.org/licenses/>.


For more details on this issue, check the COPYING file.

Installation:
=============
The instructions may vary in the different OS but we encourage to run this program under Linux as some utilities may behave unstably.

Under Linux (Debian based, including Ubuntu)
-------------------------------------------
As of August 16th, 2015, a ppa repository has been added to let users keep track of updates using the packaging utilities provided by Debian/Ubuntu systems.

1.- Adding the i3visio repository and updating the package list
```
# Adding the repository
sudo add-apt-repository ppa:i3visio
# Updating the package list
sudo apt-get update
```

2.- Installing the application and the corresponding dependencies:
```
# Official package
sudo apt-get install python-osrframework
# Installing Python dependencies manually
sudo pip install mechanize Skype4Py argparse requests python-emailahoy BeautifulSoup pyexcel pyexcel_ods pyexcel_xls pyexcel_xlsx pyexcel_text pyexcel_io tweepy matplotlib networkx decorator
```
There might be an issue in some Debian systems regarding the usage of the ouath library as v0.7.1 or later is required and in some Debian systems this library is owned by the OS.
```
Traceback (most recent call last):
  File "usufy.py", line 49, in <module>
    import osrframework.utils.platform_selection as platform_selection
  File "/usr/local/lib/python2.7/dist-packages/osrframework-0.9.10-py2.7.egg/osrframework/utils/platform_selection.py", line 277, in <module>
    from osrframework.wrappers.twitter import Twitter
  File "/usr/local/lib/python2.7/dist-packages/osrframework-0.9.10-py2.7.egg/osrframework/wrappers/twitter.py", line 32, in <module>
    from osrframework.api.twitter_api import TwitterAPIWrapper as TwitterAPIWrapper
  File "/usr/local/lib/python2.7/dist-packages/osrframework-0.9.10-py2.7.egg/osrframework/api/twitter_api.py", line 26, in <module>
    import tweepy #https://github.com/tweepy/tweepy
  File "/usr/local/lib/python2.7/dist-packages/tweepy/__init__.py", line 16, in <module>
    from tweepy.auth import OAuthHandler, AppAuthHandler
  File "/usr/local/lib/python2.7/dist-packages/tweepy/auth.py", line 9, in <module>
    from requests_oauthlib import OAuth1Session, OAuth1
  File "/usr/local/lib/python2.7/dist-packages/requests_oauthlib/__init__.py", line 3, in <module>
    from .oauth2_auth import OAuth2
  File "/usr/local/lib/python2.7/dist-packages/requests_oauthlib/oauth2_auth.py", line 3, in <module>
    from oauthlib.oauth2 import is_secure_transport
ImportError: cannot import name is_secure_transport
```
In the case of receiving a similar error to this one, we should remove the old oauth library and install the most recent version of it from pip:
```
# Hack extracted from: <http://stackoverflow.com/questions/25676259/cant-import-is-secure-transport>
#Remove old oauthlib package
sudo apt-get remove python-oauthlib

# ... and install last oauthlib version 0.7.1
pip install oauthlib -U
```

Thus, whenever a new version is released, the following command will upgrade the package:
```
sudo apt-get upgrade
```
You should be able to launch usufy.py, entify.py and so on from a terminal by typing:
```
usufy.py -h
searchfy.py -h
entify.py -h
...
```

3.- You will be able to import the .mtz configuration for Maltego from the file under:
```
/usr/share/osrframework
```

Under Linux (for developers and other systems)
----------------------------------------------

As Python is already installed, the rest of the installation under Python 2.7 is as 
follows:

1.- Download the repository. You have several options:
```
# Cloning the repository if you have git installed
git clone http://github.com/i3visio/osrframework osrframework-master
# Navigate to the destiny's folder
cd osrframework-master
```
or
```
# Download
wget http://github.com/i3visio/osrframework/archive/master.zip
# Unzip
unzip osrframework-master.zip
# Navigate to the destiny's folder
cd osrframework-master
```

2.- [Optional] Then, you might have to copy the sample files in the osrframework folder to add 
your own API Keys. You might edit them with your preferred text editor. The files are:
```
cp osrframework/utils/config_api_keys.py.sample osrframework/utils/config_api_keys.py
```
Then you can edit it with:
```
nano osrframework/utils/config_api_keys.py
```
If you skip this step, OSRFramework will create files without any credentials. This is not a
major issue as you will be able to provide them as a parameter. Then you can resume the 
installation.

3.- [Optional] Then, you might have to copy the sample files in the osrframework folder to add 
your own credentials. You might edit them with your preferred text editor. The files are:
```
cp osrframework/utils/config_credentials.py.sample osrframework/utils/config_credentials.py
```
Then you can edit it with:
```
nano osrframework/utils/config_credentials.py
```
If you skip this step, OSRFramework will create files without any credentials. This is not a
major issue as you will be able to provide them as a parameter. Then you can resume the 
installation.

4.- Then you can resume the installation.
```
# Superuser privileges are required so as to complete the installation.
sudo python setup.py build
sudo python setup.py install	
# Installing other packages from PyPI that osrframework needs using the requirements.txt file
sudo pip install -r requirements.txt
```
Afterwards, the module will be importable from any python code. You can check this by typing:
```
python -c "import osrframework"
```
If no error is displayed, the installation would have been performed correctly.

5.- To configure the Maltego Entities, launch the built-in configurator:
```
python configure_maltego.py
```
This will create a new .mtz file under: 
```
<INSTALLATION_FOLDER>/osrframework/transforms/lib/
```

6.- However, to use our Maltego Transforms, you will have to download Maltego from 
Paterva's site: 
```
http://www.paterva.com/web6/products/download2.php
```
Follow the instructions there. Afterwards, you may launch the application.

7.- You will have to import the recently created .mtz configuration file. Select 
all the groups and click next. You may use the new i3visio entities now.

Under Windows (experimental)
----------------------------
First of all, you will have to download and install Python 2.7 from:
https://www.python.org/downloads/

The installation should be performed normally. However, you will need
to add c:\python27 to the system's path variable. You have a tutorial
here: <http://earthwithsun.com/questions/441106/how-do-i-add-c-python27-to-systems-path>

You can check how everything went by accessing the cmd. Type
```
python
```
If you have accessed the Python interpreter, those are good news.

The rest of the installation under Python 2.7 is as follows:

1.- Download the latest version of the osrframework found in:
```
http://github.com/i3visio/osrframework/archive/master.zip
```

2.- Unzip the master.zip file wherever you want.

3.- [Optional] Then, you might have to copy the sample files in the osrframework folder to add 
your own API Keys. You might edit them with your preferred text editor. The files are:
```
osrframework/utils/config_api_keys.py.sample 
```
which should be COPIED to 
```
osrframework/utils/config_api_keys.py
```
If you skip this step, OSRFramework will create files without any credentials. This is not a
major issue as you will be able to provide them as a parameter. Then you can resume the 
installation.

4.- [Optional] Then, you might have to copy the sample files in the osrframework folder to add 
your own credentials. You might edit them with your preferred text editor. The files are:
```
osrframework/utils/config_credentials.py.sample 
```
which should be COPIED to 
```
osrframework/utils/config_credentials.py
```
If you skip this step, OSRFramework will create files without any credentials. This is not a
major issue as you will be able to provide them as a parameter. Then you can resume the 
installation.

5.- Open the terminal (cmd) and navigate to the recently created folder. You know something like:
```
cd Downloads
cd osrframework-master
...
```

6.- In the osrframework-master folder, build and install the modules in your system:
```
python setup.py build
python setup.py install
```
Installing other packages from PyPI that osrframework needs using the requirements.txt file. You 
should have pip installed and the path c:\python27\scripts in the system's path.
```
pip install -r requirements.txt
```
Afterwards, the module will be importable from any python code. You can check this by typing:
```
python -c "import osrframework"
```
If no error is displayed, the installation would have been performed correctly.

7.- To configure the Maltego Entities, launch the built-in configurator:
```
python configure_maltego.py
```
This will create a .mtz file under: 
```
<INSTALLATION_FOLDER>/osrframework/transforms/lib/
```

8.- However, to use our Maltego Transforms, you will have to download Maltego from 
Paterva's site: 
```
http://www.paterva.com/web6/products/download2.php
```
Follow the instructions there. Afterwards, you may launch the application.

9.- Finally, you will have to import the recently created .mtz configuration file. 
Select all the groups and click next. You may use the new i3visio entities now.

EXTRA: creating the binary packages
===================================
```
# First updating the .mtz file
python configure_maltego.py -i /usr/bin -o linux
python setup.py --command-packages=stdeb.command bdist_deb
# The deb file is under ./deb_dist
python setup.py bdist --format=zip
# The zip file is under ./dist
```
