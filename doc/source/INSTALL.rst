.. _ref_install:

============
Installation
============

To install the PyEMMA Python package, you need a few Python package dependencies. If these dependencies are not
available in their required versions, the installation will fail. We recommend one particular way for the installation
that is relatively safe, but you are welcome to try another approaches if you know what you are doing.


Anaconda install (Recommended)
==============================

We strongly recommend to use the Anaconda scientific python distribution in order to install
python-based software, including pyEMMA. Python-based software is not trivial to distribute
and this approach saves you many headaches and problems that frequently arise in other installation
methods. You are free to use a different approach (see below) if you know how to sort out problems,
but play at your own risk.

If you already have a conda installation, directly go to step 3:

1. Download and install miniconda for Python 2.7, 32 or 64 bit depending on your system:

   http://conda.pydata.org/miniconda.html

   select **yes** to add conda to the **PATH** variable.

2. If you have installed from a Linux shell, either open a new shell to have an updated PATH,
   or update your PATH variable by ``source ~/.bashrc`` (or .tcsh, .csh - whichever shell you are using).

3. Add the omnia-md software channel, and install (or update) pyemma:

   .. code::

      conda config --add channels http://conda.binstar.org/omnia
      conda install binstar # to be able to get packages from binstar
      conda install pyemma

   if the command conda is unknown, the PATH variable is probably not set correctly (see 1. and 2.)

4. Check installation:

   .. code::

      conda list

   shows you the installed python packages. You should find a pyemma 1.2 (or later)
   and ipython, ipython-notebook 3.1 (or later). If ipython is not up to date, you can still use pyemma,
   but you won't be able to load our example notebooks. In that case, update it by

   .. code::

      conda install ipython-notebook



Python Package Index (PyPI)
===========================

If you do not like Anaconda for some reason you should use the Python package
manager **pip** to install. This is not recommended, because in the past,
various problems have arisen with pip in compiling the packages that pyEMMA depends upon.

1. If you do not have pip, please read the install guide:
   `install guide <http://pip.readthedocs.org/en/latest/installing.html>`_.

2. Make sure pip is enabled to install so called
   `wheel <http://wheel.readthedocs.org/en/latest/>`_ packages:

   ::

      pip install wheel

   Now you are able to install binaries if you use MacOSX or Windows. At the
   moment of writing PyPI does not support Linux binaries at all, so Linux users
   have to compile by themselves.

3. Install pyEMMA using

   ::

      pip install pyemma

4. Check your installation

   ::

      python
      >>> import pyemma
      >>> pyemma.__version__

   should print 1.2 or later

   ::

      >>> import IPython
      >>> IPython.__version__

   should print 3.1 or later. If ipython is not up to date, update it by ``pip install ipython``


Building from Source
====================
If you refuse to use Anaconda, you will build pyEMMA from the
source. In this approach, all pyEMMA dependencies will be built from the source too.
Building these from source is sometimes (if not usually) tricky, takes a
long time and is error prone - though it is **not** recommended nor supported
by us. If unsure, use the anaconda installation.

1. Ensure that you fulfill the following prerequesites:

   * C/C++ compiler
   * setuptools > 3.6
   * cython >= 0.22
   * numpy >= 1.6
   * scipy >= 0.11
   * matplotlib >= 1.4

   If you do not fulfill these requirements, try to upgrade all packages:

   ::

       pip install --upgrade setuptools
       pip install --upgrade cython
       pip install --upgrade numpy
       pip install --upgrade scipy
       pip install --upgrade matplotlib
       
   Note that if pip finds a newer version, it will trigger an update which will
   most likely involve compilation.
   Especially NumPy and SciPy are hard to build. You might want to take a look at
   this guide here: http://www.scipy.org/scipylib/building/

2. The build and install process is in one step, as all dependencies are dragged in
via the provided *setup.py* script. So you only need to get the source of Emma
and run it to build Emma itself and all of its dependencies (if not already
supplied) from source.

   ::

      pip install pyemma


For Developers
==============
If you are a developer, clone the code repository from github and install it as follows

1. Ensure the Prerequesites (point 1) described for "Building from Source" above.

2. Make a suitable directory, and inside clone the reposity via

   ::

      git clone https://github.com/markovmodel/PyEMMA.git

3. install pyemma via

   ::

      python setup.py develop [--user]

   The develop install has the advantage that if only python scripts are being changed
   e.g. via an pull or a local edit, you do not have to reinstall anything, because
   the setup command simply created a link to your working copy. Repeating point 3 is
   only necessary if any of pyEMMA's C-files change and need to be rebuilt.

Frequently Asked Questions (FAQ)
================================

* Q: Installation went fine with conda, but import pyemma leads to the following error: ::
   
       ImportError: No module named PySide
       
  A: install pyside manually with conda::
     
     conda install pyside

* Q: My conda installation raises errors during import

  A: check if you have a file called 'easy-install.pth' in our home directory

     ~/.local/lib/python2.7/site-packages/easy-install.pth

     and validate it contains only packages you want (eg. Python packages you
     have installed with pip prior the usage of Anaconda/miniconda. If the list
     in this file contains important dependencies of PyEMMA like SciPy or NumPy
     this can cause trouble, since these packages are being used in favour of
     the conda installation and are not compatible.
     You should also make sure that this file does not contain a reference to
     the systems provided python installation like /usr/lib/python etc. because
     of the same reason.

