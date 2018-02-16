# Scratch Directory Use

Slurm creates /scratch/$SLURM\_JOB\_ID when your job is running. If you want to modify or use this output, you could include something like this in your job script:

```
SCRATCH="/scratch/$SLURM_JOB_ID"
cp $HOME/workfile.txt $SCRATCH
cd $SCRATCH

# run commands, do things

cp resultfile.txt $HOME
```



