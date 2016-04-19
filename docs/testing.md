# Running ws_event_sampler

Read until works by streaming data from minKNOW during a run to an external analysis pipeline and receiving instructions to reject reads as required. The program streaming the data is called ws_event_sampler.exe and this is found in the folder

    C:\grouper\binaries\bin

which is available after installing minKNOW.

First navigate to this folder:

    cd \grouper\binaries

ws_event_sampler can run either stand alone in simulation mode, or alongside minKNOW as it is running. For simulations, we suggest you start minKNOW and have it open (but not actually sequencing). Then start ws_event_sampler in simulation mode. In this way you will see the output from our scripts in the minKNOW messages window.

Running ws_event_sampler is done as follows:

    bin\ws_event_sampler.exe

*** NOTE: The command itself is bin\ws_event_sampler.exe so the command is executed from the folder binaries, not from within the folder bin. Executing the file from within the bin folder will result in the program crashing with a message about being unable to open a config file.

*** NOTE: ws_event_sampler provides no visible indication that it is running other than blocking the command line. If it fails, it will terminate - sometimes with an error message, but often not. Support for ws_event_sampler is available direct from ONT. We hope we have provided sufficient guidance for its use in the context of our scripts here.

ws_event_sampler can be run in simulation mode to facilitate the development of analysis scripts. When running in simulation mode, ws_event_sampler provides reads driven from a model file stored locally. This same model file must be used to analyse data when in simulation mode. When streaming live data direct from minKnow it is essential to use the correct model for the chemistry and pore type in use.

The read until API provides comprehensive instructions on how to run ws_event_sampler. Below we provide worked examples for our scripts.

To test that ws_event_sampler is functioning correctly, do the following:

1) Open a command window as administrator - to do this, right click on the cmd icon and select "Run as Administrator"

2) In this window navigate to C:\grouper\binaries

3) To see help for ws_event_sampler type:

    bin\ws_event_sampler.exe -h

which will output:

    Usage: ws_event_sampler [Options]

    Common options:
      -h [ --help ]                         Produce help message
      -c [ --config ] arg (=./conf/global.conf)
                                            Application config file.

    Specific options:
      -p [ --port ] arg                     Port to listen for requests. If this is
                                            not specified it is taken from the
                                            ws_event_sampler_port field in the
                                            config file.
      -s [ --sim ]                          Start in standalone simulation mode.
      --sim-channels arg                    Number of channels simulation uses.
                                            E.g. use a low number when debugging to
                                            make the pushed data manageable. This
                                            overrides the channel_count setting in
                                            the conf file but only during
                                            simulation.
      --sim-model arg                       Path to model file to be used by
                                            simulation when generating events.
      --sim-fasta arg                       Path to fasta file from which to draw
                                            fragments to be used by simulation.
      --sim-delay arg (=0)                  Seconds delay before starting
                                            simulation. By default the simulation
                                            starts as soon as this server starts
                                            up.
      --sim-fragment-length arg             Random lengths are bounded, approximate
                                            normal distributions, picked by rolling
                                            lots of dice. You need to specify die
                                            sides, die count and a base amount. For
                                            example, the default setting of '5 250
                                            500' will generate reads with mean
                                            length 1000 and bounds [500,1500].
      --sim-log arg                         Filename to use for csv-format log of
                                            the simulation. Will overwrite if
                                            already exists.

To set up a simulation on a specific port type:

    bin\ws_event_sampler.exe -p 9200 -s --sim-channels 100 --sim-fasta C:\path\to\RUscripts\J02459.fasta --sim-log log.txt

This will establish the data stream on port 9200, simulating 100 channels with a read distribution as described derived from the lambda sequence we have provided here. ws_event_sampler in simulation mode will write out a log file to log.txt enabling tracking of events.

First navigate to the correct folder:

    cd \path\to\RUscripts\ReadUntil

In the example.py script, edit the line which states:

    host="ws://localhost:<port>"

to

    host="ws://localhost:9200"

Note - you can specify a different port value if you wish.

Then from another command window execute the examply.py script (note this is supplied by the ONT API).

Then run the example script:

    python example.py

This should output something like (depending on the version of the API in use):

    Client connection started. Beginning unblock loop...
    channel_name= 344  read_number= 12  events_in_sample= 200  first event: start= 1104931.0  mean= 71.1864189873
    channel_name= 345  read_number= 12  events_in_sample= 200  first event: start= 1111035.0  mean= 68.1394555562
    channel_name= 346  read_number= 12  events_in_sample= 200  first event: start= 1104312.0  mean= 67.1975140682
    channel_name= 347  read_number= 15  events_in_sample= 200  first event: start= 1203518.0  mean= 72.436242832
    channel_name= 340  read_number= 12  events_in_sample= 200  first event: start= 1104326.0  mean= 60.9232571465
    channel_name= 341  read_number= 12  events_in_sample= 200  first event: start= 1102520.0  mean= 69.496870232
    channel_name= 342  read_number= 12  events_in_sample= 200  first event: start= 1097286.0  mean= 65.2731245584
    channel_name= 343  read_number= 12  events_in_sample= 200  first event: start= 1102224.0  mean= 65.2680067692
    channel_name= 348  read_number= 12  events_in_sample= 200  first event: start= 1119138.0  mean= 77.3645669056
    channel_name= 349  read_number= 12  events_in_sample= 200  first event: start= 1092464.0  mean= 72.4693304753
    channel_name= 298  read_number= 12  events_in_sample= 200  first event: start= 1109404.0  mean= 66.3816659282
    channel_name= 299  read_number= 12  events_in_sample= 200  first event: start= 1103390.0  mean= 66.1452746381

If you see:

    Client connection started. Beginning unblock loop...
    Unhandled exception in thread started by <bound method ReadUntil.data_received_own_thread of <read_until.ReadUntil object at 0x00000000023AA
    FD0>>
    Traceback (most recent call last):
    File "C:\...\ReadUntil\read_until.py", line 110, in data_received_own_thread
    self.data_received(channels_update)
    File "example.py", line 46, in data_received
    for channel_id, data in channels.iteritems():
    AttributeError: 'NoneType' object has no attribute 'iteritems'
    Unhandled exception in thread started by <bound method ReadUntil.data_received_own_thread of <read_until.ReadUntil object at 0x00000000023AA
    FD0>>
    Traceback (most recent call last):
    File "C:\...\ReadUntil\read_until.py", line 110, in data_received_own_thread
    self.data_received(channels_update)
    File "example.py", line 46, in data_received
    for channel_id, data in channels.iteritems():
    AttributeError: 'NoneType' object has no attribute 'iteritems'
    Unhandled exception in thread started by <bound method ReadUntil.data_received_own_thread of <read_until.ReadUntil object at 0x00000000023AA
    FD0>>

Then you have likely got a clash between the API version we have specified and the version of minKNOW installed.
