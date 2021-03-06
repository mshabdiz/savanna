Savanna Installation Guide
==========================

We recommend you install in a way that will can keep your system in a
consistent state. Ways we recommend to install Savanna are:

* Install via `Fuel <http://fuel.mirantis.com/>`_

* Install via `RDO Havana+ <http://openstack.redhat.com/>`_

* Install into virtual environment



To install with Fuel
--------------------

1. Start by following `Quickstart <http://software.mirantis.com/quick-start/>`_
   to install and setup OpenStack

2. Enable Savanna service during installation



To install with RDO
-------------------

1. Start by following the `Quickstart
   <http://openstack.redhat.com/Quickstart>`_ to install and setup
   OpenStack.

2. Install the savanna-api service with,

.. sourcecode:: console

     $ yum install openstack-savanna
..

3. Configure the savanna-api service to your liking. The configuration
   file is located in ``/etc/savanna/savanna.conf``.

4. Start the savanna-api service with,

.. sourcecode:: console

     $ service openstack-savanna-api start
..


To install into a virtual environment
-------------------------------------

1. First you need to install `python-setuptools`, `python-virtualenv` and python headers using your
   OS package manager. The python headers package name depends on OS. For Ubuntu it is `python-dev`,
   for Red Hat - `python-devel`. So for Ubuntu run:

.. sourcecode:: console

    $ sudo apt-get install python-setuptools python-virtualenv python-dev
..

   For Fedora:

.. sourcecode:: console

    $ sudo yum install gcc python-setuptools python-virtualenv python-devel
..

   For CentOS:

.. sourcecode:: console

    $ sudo yum install gcc python-setuptools python-devel
    $ sudo easy_install pip
    $ sudo pip install virtualenv

2. Setup virtual environment for Savanna:

.. sourcecode:: console

    $ virtualenv savanna-venv
..

   This will install python virtual environment into ``savanna-venv`` directory
   in your current working directory. This command does not require super
   user privileges and could be executed in any directory current user has
   write permission.

3. You can install the latest Savanna release version from pypi:

.. sourcecode:: console

    $ savanna-venv/bin/pip install savanna
..

   Or you can get Savanna archive from `<http://tarballs.openstack.org/savanna/>`_ and install it using pip:

.. sourcecode:: console

    $ savanna-venv/bin/pip install 'http://tarballs.openstack.org/savanna/savanna-master.tar.gz'
..

   Note that savanna-master.tar.gz contains the latest changes and might not be stable at the moment.
   We recommend browsing `<http://tarballs.openstack.org/savanna/>`_ and selecting the latest stable release.

4. After installation you should create configuration file. Sample config file location
   depends on your OS. For Ubuntu it is ``/usr/local/share/savanna/savanna.conf.sample-basic``,
   for Red Hat - ``/usr/share/savanna/savanna.conf.sample-basic``. Below is an example for Ubuntu:

.. sourcecode:: console

    $ mkdir savanna-venv/etc
    $ cp savanna-venv/share/savanna/savanna.conf.sample-basic savanna-venv/etc/savanna.conf
..

    check each option in savanna-venv/etc/savanna.conf, and make necessary changes

5. Create database schema:

.. sourcecode:: console

    $ savanna-venv/bin/python savanna-venv/bin/savanna-db-manage --config-file savanna-venv/etc/savanna.conf upgrade head
..

6. To start Savanna call:

.. sourcecode:: console

    $ savanna-venv/bin/python savanna-venv/bin/savanna-api --config-file savanna-venv/etc/savanna.conf
..


Note:
-----
One of the :doc:`Savanna features <features>`, Anti-Affinity, requires a Nova adjustment.
See :ref:`Enabling Anti-Affinity <enable-anti-affinity>` for details. But that is purely optional.


Make sure that your operating system is not blocking Savanna port (default: 8386).
You may need to configure iptables in CentOS and some other operating systems.

   To get the list of all possible options run:

.. sourcecode:: console

    $ savanna-venv/bin/python savanna-venv/bin/savanna-api --help


Further consider reading :doc:`overview` for general Savanna concepts and
:doc:`plugins` for specific plugin features/requirements
