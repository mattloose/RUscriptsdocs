#Getting started

We provide two sets of scripts. The first set are "Offline" scripts. They do not require the Read Until API and so can be run on any platform.

The second set (ONLINE scripts) absolutely require the API. For these *you must have minKNOW installed on the windows machine you are running this code on.*

We assume that you are running these scripts on a windows machine with minKNOW installed. ONT install a version of python called Anaconda alongside minKNOW and this python version comes with some of the required packages for our scripts. Our scripts will also run on Linux or OSX but at this time we provide no explicit documentation to support this, however users confident with python and Unix should have no problems.

To use read until at this time you have to use the command line. To access the command line on windows, click on the start menu and type 'cmd' in the search box. You should see a program called 'cmd'.

Once at the command line, navigate to the folder containing this Readme file.

    > cd \path\to\RUscripts

All scripts are python 2.7.

We assume that the default version of python in your path is the ONT Anaconda installation. To test this, type

    > python

And you should see:

    Python 2.7.5 |Anaconda 1.8.0 (64-bit)| (default, Jul  1 2013, 12:37:52) [MSC v.1500 64 bit (AMD64)] on win32
    Type "help", "copyright", "credits" or "license" for more information.
    >>>

Note that this shows Anaconda 1.8.0

To exit this window type

    >>> exit()

Please note these scripts depend upon APIs which are not provided here. The Read Until API is available from Oxford Nanopore on request to MAP participants.

#Installing components for Read Until Scripts

Python modules required for running read until using source code.

* thrift
* ws4py
* h5py
* configargparse
* biopython
* watchdog
* psutil
* mlpy # Must be version 3.5.0 or above - cannot be installed with easy_install/pip on Windows - see below for details
* sklearn # Available as default with Anaconda



To install these modules on the ONT Anaconda type:



    > easy_install thrift ws4py h5py configargparse biopython watchdog psutil

NOTE: You may need to add C:\Anaconda\Scripts to your path to access easy_install and pip.

To install mlpy

Installing mlpy with easy_install results in a version less than that required. To overcome this on windows systems visit [http://www.lfd.uci.edu/~gohlke/pythonlibs/#mlpy](http://www.lfd.uci.edu/~gohlke/pythonlibs/#mlpy) to obtain an mlpy wheel compiled for the appropriate version of windows and python.

On our system this file is called:

mlpy-3.5.0-cp27-none-win_amd64.whl


To install this you need to first install pip.

    > easy_install install pip

Then to install your downloaded wheel:

    > pip install \path\to\mlpy-3.5.0-cp27-non-win_amd64.whl

Now you should have all the prerequisites required to run these scripts on windows using the native python.


# Obtaining the Read Until API

The read until API is available on request from Oxford Nanopore Technologies to individuals who are members of the MAP. Please see the ONT Store/WIKI or contact your ONT representative for further assistance.

We remind you again:

*Important Note: Running read until will influence the behaviour of your flow cell and change the output of your sequencing experiment. You are strongly advised to run simulations of read until prior to running on a live flow cell. The code as presented here is a demonstration of read until and one method by which it can be implemented. Users run this code entirely at their own risk.*

# Installing the API

Once you have obtained the API, copy the following files and folders (and contents) into the RUscripts\ReadUntil folder:

    read_until.py
	event_sampler.thrift
    event_sampler/* (note - you need to copy the folder and its contents)
    example.py


# API versions

The read until API changes depending on the version of minKNOW in use. The read until API for minKNOW versions 0.48.1.3 - 0.51.1.51 is available on request from Oxford Nanopore.  

Our code is compatible with all versions of the API. However, the latest version of minKNOW as of 4th April 2016 does not function as anticipated. It will work for simulation runs with ws_event_sampler, but minKNOW itself does not function correctly with the API. This is actively being resolved by ONT. Thus, testing and simulation is possible with our code and later versions of minKNOW and ws_event_sampler but these scripts WILL NOT WORK AT THIS TIME with minKNOW versions > 0.51.1.51
