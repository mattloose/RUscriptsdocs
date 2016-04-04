# Files and Folders

Below is a list of all the files and folders required for running read until.

* ampbalance.py - an illustrative script for selecting a fixed number of reads from individual amplicons using squiggle matching alone.

* ampbalancetest (folder - contains 110 example fast5 files)

* ampliconSPLIT.py - an illustrative script that will split reads into folders based on squiggle matching to individual amplicons.

* exampleread\llssbzms2p35x_lambda11ladderup_1208_1_ch11_file27_strand.fast5 - An example read for the extraction of template and complement model files. Note this read is derived from the R7 chemistry.

* getmodels.py - A script for extracting model files to generate a squiggle reference for a given sequence.

* J02459.fasta - A reference fasta file for bacteriophage lambda. This is the reference used for all our work.

* lambda_amplicons.txt - A file that defines the amplicons used in this study. The file is in the format seq_id:start-stop - so here the seq_id is J02456 (as in the file J02459.fasta) and the start and stop coordinates match our amplicons eg. J02456:52-1980

* LICENSE - MIT License

* README.md - this readme file.

* ReadUntil\aReadUntil.py - A script for amplicon balancing via the read until API.

* ReadUntil\gReadUntil.py - A script for selecting a specific region of the genome via the read until API

* ReadUntil\lambda_amplicons.fasta - This is a reference file containing copies of individual amplicons for bacteriophage lambda. It is used in testing the behaviour of aReadUntil.py - described below.

* ReadUntil\ruutils.py - This file contains a number of useful functions for various scripts. It will never be run itself but is called by many of the other scripts.

* test_gReadUntil.py - A script for testing the functionality of gReadUntil.py in the absence of the API itself.

* RUtestset (folder - contains 55 example fast5 files)
