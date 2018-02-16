# Batch Scripts

Batch jobs can be submitted on the Lawrence cluster using Slurm commands. A variety of configurations can be used for formulating a batch script. To access the GPU/vis/himem nodes, please see the previous corresponding pages for the batch commands to include. A basic batch script will look like the one below:

```
#!/bin/bash

#SBATCH -N 10
#SBATCH -q regular
#SBATCH -J example1
#SBATCH --mail-user=user.name@coyotes.usd.edu
#SBATCH --mail-type=ALL
#SBATCH -t 12:00:00

#OpenMP settings:
export OMP_NUM_THREADS=1
export OMP_PLACES=threads
export OMP_PROC_BIND=spread

#run the application after this line##########################
srun -n 10 -c 48 --cpu_bind=cores /share/apps/someapp
```





