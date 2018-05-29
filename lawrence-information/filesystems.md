# Filesystems

##### Home Directories

Home directories have 50GB of storage. Additionally, home directories are shared across nodes and have a path as follows:

```
/home/usd.local/user.name

###Home directories can also be called by their environmental variable:

$HOME
```

Please note that home directories are not backed up!

##### Group Home DIrectories

Group home directories have 5TB of storage. Additionally, home directories are shared across nodes and have a path as follows:

```
/home/smith-lab
    /shared (read/write permissions for all group members)
```

Please note that group home directories are not backed up!

##### Scratch

Slurm creates /scratch/job\_$SLURM\_JOB\_ID when your job is running. If you want to modify or use this output, you could include something like this in your job script:

```
SCRATCH="/scratch/job_$SLURM_JOB_ID"
cp $HOME/workfile.txt $SCRATCH
cd $SCRATCH

# run commands, do things

cp resultfile.txt $HOME
```

Please note that /scratch is not a shared filesystem and that each node has its own /scratch \(169 GB per node \(SSD\)\). Additionally, the data on scratch only lasts while the job is running! If you need /scratch data from your job, remove it before your job ends.

# 



