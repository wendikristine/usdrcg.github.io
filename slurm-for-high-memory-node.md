# High-Memory Node

The Lawrence high-memory \(himem\) node has two partitions, each with 1.5 TB of RAM. This node is especially useful for jobs requiring a large amount of memory and can be accessed either interactively or with a batch script.

For interactive jobs on the Lawrence himem nodes, use the srun command as follows:

```
[user.name@usd.local@login ~]$ srun --pty -p himem bash
[user.name@usd.local@himem02 ~]$
```

To use the high memory node within a batch job, add “--partition=himem” to your script.

Below is an example batch script which calls the a high-memory node. This template can be followed when requesting the himem node on Lawrence:

```
#!/bin/bash

# Example job submission script
# This is a comment.
# Lines beginning with the # symbol are comments and are not interpreted by
# the Job Scheduler.
# Lines beginning with #SBATCH are special commands to configure the job.

### Job Configuration Starts Here #############################################
# Export all current environment variables to the job (Don't change this)
#SBATCH --get-user-env
# The default is one task per node
#SBATCH --ntasks=1
#SBATCH --nodes=1
# Request a high memory node
#SBATCH --partition=himem
# Request all memory on the node
#SBATCH --mem=0
#request 10 minutes of runtime - the job will be killed if it exceeds this
#SBATCH --time=10:00
# Change email@example.com to your real email address
#SBATCH --mail-user=email@example.com
#SBATCH --mail-type=ALL

### Commands to run your program start here ####################################
pwd
echo "Hello, World!"
sleep 5
```





