# Slurm

The Slurm Workload Manager is the job scheduler used by the Lawrence HPC. For a comprehensive overview of Slurm commands, visit the slurm webpage:[https://slurm.schedmd.com/quickstart.html](https://slurm.schedmd.com/quickstart.html)

For the commonly used Slurm commands on the Lawrence HPC, we have provided quick-start documentation with examples within the Wiki.

# Interactive Jobs

##### General Compute

INteractive sessions on compute nodes can be used with the Slurm command "srun". For the use of one node, this command can be used generally as demonstrated below:

```
[user.name@usd.local@login ~]$ srun --pty bash
[user.name@usd.local@node37 ~]$ 
```

##### HiMem

The Lawrence high-memory \(himem\) node has two partitions, each with 1.5 TB of RAM. This node is especially useful for jobs requiring a large amount of memory and can be accessed either interactively or with a batch script.

For interactive jobs on the Lawrence himem nodes, use the srun command as follows:

```
[user.name@usd.local@login ~]$ srun --pty -p himem bash
[user.name@usd.local@himem02 ~]$
```

##### GPU

For interactive GPU sessions, a gpu node is requested as below \(Note: you will be assigned one of the two GPU nodes\):

```
[user.name@usd.local@login ~]$ srun --pty -p gpu bash
[user.name@usd.local@gpu01 ~]$ 
```

# Batch Jobs

##### General Compute

Batch jobs can be submitted on the Lawrence cluster using Slurm commands. A variety of configurations can be used for formulating a batch script. A basic batch script will look like the one below:

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

##### HiMem

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

##### GPU

Below is an example batch script which calls the GPU nodes, this template can be followed when requesting 1 or 2 GPU nodes on Lawrence:

```
#!/bin/bash

# template.slurm: Example job submission script
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
# Request 1 GPU
# Each gpu node has two logical GPUs, so up to 2 can be requested per node
# To request 2 GPUs use --gres=gpu:pascal:2
#SBATCH --partition=gpu
#SBATCH --gres=gpu:pascal:1
#request 10 minutes of runtime - the job will be killed if it exceeds this
#SBATCH --time=10:00
# Change email@example.com to your real email address
#SBATCH --mail-user=email@example.com
#SBATCH --mail-type=ALL

### Commands to run your program start here ####################################
pwd
echo "Hello, World!"
sleep 5
nvidia-smi
```

## Graphical User Interface Jobs \(VNC\)

##### General Compute

##### HiMem

##### GPU

GPU nodes must be specifically requested using the “--gres” parameter. GPU access is controlled by cgroups, which means the resource must be requested if it is to be used. This prevents use conflicts. The format for requesting a GPU node \(as specified in the contig file\) is TYPE:LABEL:NUMBER.

TYPE will be “gpu”.

LABEL is defined as “pascal” for the GPU node.

NUMBER is the amount of resources requested. For the GPU node, there are two logic units, so a user can request “1” or “2”.

An example command would be as follows:

```
srun --pty --gres=gpu:pascal:2 --partition=gpu /bin/bash
```

To see which GPUs are available use the following command:

```
nvidia-smi
```

##### Vis

Vis nodes must be specifically requested using the “--gres” parameter. Vis access is controlled by cgroups, which means the resource must be requested if it is to be used. This prevents use conflicts. The format for requesting a GPU node \(as specified in the contig file\) is TYPE:LABEL:NUMBER.

TYPE will be “vis”.

LABEL is defined as “gtx” for the viz node.

NUMBER is the amount of resources requested. For the Vis node the only option is “1” as there is only one.

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

Group home directories have no additional storage. Additionally, home directories are shared across nodes and have a path as follows:

```
/home/smith-lab
    /shared (read/write permissions for all group members)
```

Please note that group home directories are not backed up!

##### Scratch

Slurm creates /scratch/$SLURM\_JOB\_ID when your job is running. If you want to modify or use this output, you could include something like this in your job script:

```
SCRATCH="/scratch/$SLURM_JOB_ID"
cp $HOME/workfile.txt $SCRATCH
cd $SCRATCH

# run commands, do things

cp resultfile.txt $HOME
```

Please note that /scratch is not a shared filesystem and that each node has its own /scratch \(169 GB per node \(SSD\)\). Additionally, the data on scratch only lasts while the job is running! If you need /scratch data from your job, remove it before your job ends.

# 



