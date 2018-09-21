# Legacy-Lawrence Migration

This article was created for users transitioning from Legacy to Lawrence during the migration process. Many new and exciting features await on the new Lawrence USD cluster including improved job management, ease of software installation \(through modules\), and hardwear to push the boundaries of your research computing experience. Below you will find a guide for transitioning to this new environment. More detailed information is also available in the Lawrence specific documentation.

##### Job Management: SGE to Slurm

The new Lawrence cluster uses Slurm for job management \(on Legacy job management is completed with Sun Grid Engine\). Below, you will find a table comparing basic command usage between Grid Engine and Slurm:

| _Command_ | _Sun Grid Engine \(Legacy\)_ | _Slurm \(Lawrence\)_ |
| :--- | :--- | :--- |
| Interactive login | qlogin | srun --pty bash |
| Job submission | qsub \[scirpt\_file\] | sbatch \[script\_file\] |
| Job deletion | qdel \[job\_id\] | scancel \[job\_id\] |
| Job status by job | qstat -u \\* \[-j job\_id\] | squeue \[job\_id\] |
| Job status by user | qstat \[-u username\] | squeue -u \[user\_name\] |
| List queue | qconf -sql | squeue |
| Cluster status | qhost -q | sinfo |
| GUI | qmon | sview |

For more detailed information on Slurm commands visit the Slurm [webpage](https://slurm.schedmd.com/).

##### Transferring Data to Lawrence from Legacy

The data in a home directory on Legacy may be transferred to Lawrence using the rsync utility. More details can be found on the Rsync [webpage](https://rsync.samba.org/).

For example, to copy the directory called data/ from Legacy to Lawrence use a command like the following - don't forget the colon at the end.

`[choover@login-0-0 ~]$ rsync -az data choover@lawrence.usd.edu:`

`Warning: Permanently added 'lawrence.usd.edu' (RSA) to the list of known hosts.`

`[choover@login-0-0 ~]$ `



