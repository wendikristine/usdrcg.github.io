# Batch Jobs

A batch job runs a program or series of programs without manual intervention. This is useful when launching complex or time-consuming jobs. Unlike interactive qlogin sessions batch jobs continue to run even if you log out. All of their output is written to a file \(or files\) instead of to the screen.

You do not need to specify which compute nodes to run the job. The `qstat` command will automatically choose an available compute node or nodes. If no suitable nodes are available, your job will be put into a wait state and will launch as soon as compute nodes are available.

## Job Submission Scripts

Batch jobs are defined in a _job submission script _and launched via the `qsub` command.

The file /share/apps/examples/template.qsub \(included below\) as a starting point for creating your own job scripts

```
# template.qsub: Example job submission script

# This is a comment.
# Lines beginning with the # symbol are comments and are not interpreted by 
# the Job Scheduler.

# Lines beginning with #$ are special commands to configure the job.
		
### Job Configuration Starts Here #############################################
# Run the job in the current working directory (Don't change this)
#$ -cwd

# Run this job in the normal Bash shell environment (Don't change this)
#$ -S /bin/bash

# Export all current environment variables to the job (Don't change this)
#$ -V

# Parallel environment and number of CPU cores
# Syntax -pe 
<
parallel_environment
>
<
cpu_cores
>

# Possible values include:
#   threaded - for shared-memory jobs running on a single compute node
#   orte     - for multi-node jobs using OpenMPI
# CPU cores: 1-32 for parallel jobs this should match what you pass to 
#   mpirun below
#
# In this example we request 1 CPU core on a single compute node
#$ -pe threaded 1
			
# Job name - this will show up in the output of the qstat command
# Don't use spaces or special characters
#$ -N myjob
					
# Output file name - all regular output goes to this file instead of the screen
#$ -o myjob-out.txt
							
# Error output file name - all Job Errors are written to this file
#$ -e myjob-err.txt

# Send email upon job end/abort/suspend to the specified address
# Possible values for -m are:
#   'b'     Mail is sent at the beginning of the job.
#   'e'     Mail is sent at the end of the job.
#   'a'     Mail is sent when the job is aborted or rescheduled.
#   's'     Mail is sent when the job is suspended.
#   'n'     No mail is sent.
# Fill in your email address and uncomment the line below to enable email
##$ -M jsmith@email.com -m eas
						
### Commands to run your program start here ####################################
# Set up environment
# Examples:
# source /share/apps/nwchem/env.sh
# source /share/apps/qiime/env.sh
# source /share/apps/openmpi/env.sh

# Run your program(s)
# NOTE: CPU count passed to "mpirun -np" must match the number erquestred via 
# the -pe parameter above.
# Examples:
# mpirun -np 4 nwchem myfile
# mpirun -np 16 /share/apps/mrbayes/mb-multi myfile.nex
# python myscript.py
echo "Hello, World!"
```

## Monitoring Batch Jobs 

All jobs are assigned a job ID and can be monitored with the `qstat` command which lists all of your running and scheduled jobs. Here is an example of user jsmith monitoring a job.

```
[jsmith@login-0-0 best]$ qstat
job-ID  prior   name   	user     	state submit/start at 	queue              slots ja-task-ID
---------------------------------------------------------------------------------------
5842    0.00000 best-jsmi     jsmith          qw	12/14/2009 12:18:07                4
```

The output of the `qstat` command shows a list of your jobs and what state they’re in. In this case there is only one job \(job 5842\) running and it is in the `qw` or "queued, waiting" state. The `qstat` command will show an 'r' for jobs that are running, and an 'e' for jobs in an error state.

To see a listing of all running and scheduled jobs for all users type

```
qstat -u '*'
```

Once a job completes, it is no longer listed in the `qstat` output.

## Canceling a Job 

To cancel a running or waiting job use the qdel command and pass it the job id of the job you’d like to terminate. You can only cancel jobs for which you are the owner. Here’s an example:

```
[jsmith@login-0-0 ~]$ qdel 5842
jsmith has registered the job 5842 for deletion
```

## Example Batch Jobs

The directory /share/apps/examples contains example batch jobs.

### Elephant

```
djennewe@login-0-0 my_examples $ cp -r /share/apps/examples/elephant .
djennewe@login-0-0 my_examples $ ls
elephant
djennewe@login-0-0 my_examples $ cd elephant
djennewe@login-0-0 elephant $ ls
elephant.py  elephant.qsub  README
djennewe@login-0-0 elephant $ qsub elephant.qsub
Your job 510127 ("elephant-job") has been submitted
djennewe@login-0-0 elephant $ qstat
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID
-----------------------------------------------------------------------------------------------------------------
 510127 0.00000 elephant-j djennewe     qw    01/19/2017 11:37:27                                    1
djennewe@login-0-0 elephant $ qstat
djennewe@login-0-0 elephant $ ls
elephant-err.txt  elephant-out.txt  elephant.png  elephant.py  elephant.qsub  README
djennewe@login-0-0 elephant $
```

You can view the output file elephant.png by copying it to your computer and opening it.

### Parallel processor NWChem

```
djennewe@login-0-0 my_examples $ cp -r /share/apps/examples/nwchem .
djennewe@login-0-0 my_examples $ ls
nwchem
djennewe@login-0-0 my_examples $ cd nwchem
djennewe@login-0-0 nwchem $ ls
nwchem-water.qsub  README  water_molecule.nw
djennewe@login-0-0 nwchem $ qsub nwchem-water.qsub
Your job 510128 ("nwchem-water-job") has been submitted
djennewe@login-0-0 nwchem $ qstat
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID
-----------------------------------------------------------------------------------------------------------------
510128 0.00000 nwchem-wat djennewe     qw    01/19/2017 11:41:36                                    4
djennewe@login-0-0 nwchem $ qstat
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID
-----------------------------------------------------------------------------------------------------------------
510128 0.51968 nwchem-wat djennewe     r     01/19/2017 11:41:46 32core128GB.q@compute-0-43.loc     4
djennewe@login-0-0 nwchem $ qstat
djennewe@login-0-0 nwchem $ ls
h2o_freq.b     h2o_freq.db          h2o_freq.hess    h2o_freq.nmode  nwchem-water-err.txt  README
h2o_freq.b^-1  h2o_freq.drv.hess    h2o_freq.movecs  h2o_freq.p      nwchem-water-out.txt  water_molecule.nw
h2o_freq.c     h2o_freq.fd_ddipole  h2o_freq.mp2nos  h2o_freq.zmat   nwchem-water.qsub
djennewe@login-0-0 nwchem $

```

  


