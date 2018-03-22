##### Legacy-Lawrence Migration Information

This article was created for users transitioning from Legacy to Lawrence during the migration process. The new Lawrence cluster uses Slurm for job management \(on Legacy job management is completed with Sun Grid Engine\). Below, you will find a table comparing command usage between Grid Engine and Slurm:



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



