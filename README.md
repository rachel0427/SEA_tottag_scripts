# SEA_tottag_scripts
Repo for TotTag proximity data scripts. 
The goal for weeks of Jan 31 and Feb 7 is to create a python script that produces the following from the testing log file:
1) Identify 'check-ins' from proximity data based off distance and time within a certain distance interval
2) Identify window of time around event (arrival time vs. departure time)
3) Identify each window of interaction by who initiates interaction (which tag from pair approaches the other and for how long)

## How to clone:
### Please refer to this handy tutorial github has created: https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository

## Don't forget to `git pull`!
Once you have your github repository set up on your local machine, **always make sure** to `git pull` before making **any changes**.
This will ensure that if someone else has contributed to the code base while you were not active, their changes are reflected in your local repository, this helps later on down the workflow pipeline when pushing code (github will give you an error if you try to push to a branch that has changes not seen in your local repo).

If you want to learn what's going on 'under the hood,' refer to: https://www.git-scm.com/docs/git-pull

## scripts/Analysis 
### (this code is from https://github.com/lab11/socitrack/tree/master/software/analysis)
Scripts used to analyze the downloaded TotTag log files. To begin, run the tottagAverager.py script, which takes at least 3 arguments: the starting Unix timestamp, the ending Unix timestamp, and a list of every log file that you would like to average together. The data is averaged accross timestamps by dyad, so the measured value at a certain timestamp from one TotTag is averaged with the value at the same timestamp from its companion TotTag. The script can be run like so:

`python tottagAverager.py START_TIME_VAL END_TIME_VAL LOG_FILE_1 LOG_FILE_2...`

Next, run the tottagSmoother.py script, which takes at least 2 arguments: the number of data points over which to smooth, followed by a list of every log file you would like to smooth. The smoother works by taking a moving average with a width of SMOOTHING_VAL. When it encounters a gap in the data greater than the aforementioned value, the smoothing buffer is cleared and it starts over after the gap. To run the script, enter:

`python tottageSmoother.py SMOOTHING_VAL AVERAGED_LOG_FILE_1 AVERAGED_LOG_FILE_2...`

Now, your data is ready to go, and you can begin running the tottagStats.py script on it. This script produces summary statistics on the smoothed log file. The statistics it outputs are the amount of time each dyad spent within 3ft of one another, the amount of time the TotTags were in range of one another, and the number of times a dyad re-enters 3ft after leaving it for at least 30 seconds. The input for this script is simply a single log file:

`python tottagStats.py SMOOTHED_LOG_FILE_1`
