=======================
Development Environment
=======================
This guide describe how to set up an environment in order to contribute to the development of GlobaLeaks.

Requirements
============
The guide assumes you run a Debian based system and that the following software is installed on your system:

.. code:: sh

   apt-get install debhelper devscripts dh-apparmor dh-python git npm python3 python3-dev python3-pip python3-setuptools python3.11-venv python3-sphinx python3-virtualenv tor-y

Then you should edit the config to enable the Tor protocol:

.. code:: sh

  sudo nano /etc/tor/torrc

Remove the # character from lines ControlPort 9051 and CookieAuthentication 1 (line ~57)
Restart Tor

.. code:: sh

  /etc/init.d/tor restart

Add permission yourself to read the auth cookie by

.. code:: sh

  /usr/sbin/usermod -a -G debian-tor [yourlinuxuser]

Setup
=====
The repository could be cloned with:

.. code:: sh

  git clone https://github.com/globaleaks/GlobaLeaks.git

Client dependencies could be installed by issuing:

.. code:: sh

  cd GlobaLeaks/client
  npm install -d
  grunt copy:sources

Backend dependencies could be installed by issuing:

.. code:: sh

  cd GlobaLeaks/backend
  python3 -mvenv env
  source ./env/bin/activate
  pip3 install -r requirements.txt

This will create for you a python virtualenv in the directory env containing all the required python dependencies.

Then, anytime you will want to activate the environment to run globaleaks you will just need to issue the command:

.. code:: sh

  cd GlobaLeaks/backend && source ./env/bin/activate

Setup the client:

.. code:: sh

  cd GlobaLeaks/client
  npm install -d
  grunt build

Setup the backend and its dependencies:

.. code:: sh

  cd GlobaLeaks/backend
  python3 -menv env
  source env/bin/activate
  pip3 install -r requirements.txt

Run
===
To run globaleaks from sources within the development environment you should issue:

.. code:: sh

  cd GlobaLeaks/backend
  source ./env/bin/activate
  ./bin/globaleaks -z -n

GlobaLeaks will start and be reachable at the following address https://127.0.0.1:8443
