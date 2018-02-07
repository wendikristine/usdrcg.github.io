# Slurm for High Memory Node

The Lawrence high-memory \(himem\) node has two partitions, each with 1.5 TB of RAM. This node is especially useful for jobs requiring a large amount of memory and can be accessed either interactively or with a batch script.

For interactive jobs on the Lawrence himem nodes, use the srun command as follows:

\[user.name@usd.local@login ~\]$ srun --pty -p himem bash

\[user.name@usd.local@himem02 ~\]$ 

To use the high memory node within a batch job, add “--partition=himem” to your script.

