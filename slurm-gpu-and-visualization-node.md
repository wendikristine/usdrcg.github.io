# GPU Nodes

GPU/Viz nodes must be specifically requested using the “--gres” parameter. GPU access is controlled by cgroups, which means the resource must be requested if it is to be used. This prevents use conflicts. The format for requesting a GPU node \(as specified in the contig file\) is TYPE:LABEL:NUMBER.

TYPE will be “gpu”.

LABEL is defined as “gtx” for the viz node and “pascal” for the GPU node.

NUMBER is the amount of resources requested. For the GPU node, there are two logic units, so a user can request “1” or “2”. For the Viz node the only option is “1” as there is only one.

An example command would be as follows:

```
srun --pty --gres=gpu:pascal:2 --partition=gpu /bin/bash
```

To see which GPUs are available use the following command:

```
nvidia-smi
```

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



