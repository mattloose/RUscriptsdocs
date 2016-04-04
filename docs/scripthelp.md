# Getting Script Help

All scripts here adhere to the following standard arguments:

* -h Will print a help statement and exit.
* -ver Will print version information and exit.
* -v Will print additional debug information and more verbose output to screen while the code is executing.

Additional options are described for each script in the documentation.

# Common Failures

1) ws_event_sampler crashes: If ws_event_sampler crashes, the read until scripts will no longer 'see' the events and thus the sequencer will sequence all reads regardless of where they map too. The scripts alert you to a dropped connection with the message "Hanging around waiting for server". You should check for this periodically. We hope that ws_event_sampler will become more stable over time. ws_event_sampler can be restarted at any point to restart capturing data.

2) Processor timeouts: If the load on the CPU is too high, reads will 'timeout'. This will result in a loss of selective sequencing.

3) Missing amplicons: If an amplicon is entirely missing from a sample, read until will never complete. It is wise to carefully observe a run and check this hasn't occurred.

#Less Common Failures

Rarely a read until script will crash. This will have different failure modes depending on the script.

gReadUntil crashes will allow all reads to be sequenced for the period of time the script is not running. Restarting the script will re enable selective sequencing.

Rarely aReadUntil.py will crash. At this time, aReadUntil does not recover from a crash such that a read until run can be continued. Essentially if the script crashes it loses track of where it was at. We hope to add this functionality in the near future. User beware. 
