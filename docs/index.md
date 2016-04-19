# Read Until

This documentation accompanies the preprint currently available [BioRxiv](http://biorxiv.org/content/early/2016/02/03/038760 "Read Until Manuscript").

The associated GitHub repository is [here](https://github.com/mattloose/RUscripts "Read Until GitHub").

Read Until is a technology enabled by the [Oxford Nanopore Technologies](http://nanoporetech.com "Oxford Nanopore Technologies Homepage") MinION and expected to be available in the future PromethION sequencers. The scripts described here provide one method of implementation of read until. The scripts are supplied as is and are used at your own risk.

#*WARNING:*

The read until API changes depending on the version of minKNOW in use. The read until API for minKNOW versions 0.48.1.3 - 0.51.1.51 is available on request from Oxford Nanopore.  

Our code is compatible with all versions of the API. However, versions of minKNOW since 0.51.1.51 and up to 4th April 2016 do not function as anticipated. The ws_event_sampler simulations will work, but minKNOW itself does not function correctly with the API. This is actively being resolved by ONT. Thus, testing and simulation is possible with our code and later versions of minKNOW and ws_event_sampler but these scripts WILL NOT ACTIVELY REJECT READS AT THIS TIME with minKNOW versions > 0.51.1.51. This is actively under investigation by ONT and updates will be posted here when this is resolved.

*You must have minKNOW installed on the windows machine you are running this code on. ONT install Anaconda, a version of python, alongside minKNOW and this comes with some of the required packages for our scripts. Our scripts will also run on Linux or OSX but at this time we provide no explicit documentation to support this, however users confident with python and Unix should have no problems.*

#*Risks!!*

Running read until will influence the behaviour of your flow cell and change the output of your sequencing experiment. You are strongly advised to run simulations of read until prior to running on a live flow cell. The code as presented here is a demonstration of read until and one method by which it can be implemented. Users run this code entirely at their own risk.

*Please note these scripts depend upon APIs which are not provided here. The Read Until API is available from Oxford Nanopore on request to MAP participants.*


#Getting help with read until.

We are happy to help where we can. Please feel free to contact via twitter [@mattloose](https://twitter.com/mattloose) or email <matt.loose@nottingham.ac.uk>. We will try to update this read me file whenever significant changes are made to the API or minKNOW versions that might affect read until. For issues with the API itself or the ws_event_sampler program, users will most likely be redirected to ONT.




<!---For full documentation visit [mkdocs.org](http://mkdocs.org).

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs help` - Print this help message.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.
-->
