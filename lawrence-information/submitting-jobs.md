# Slurm

The Slurm Workload Manager is the job scheduler used by the Lawrence HPC. For a comprehensive overview of Slurm commands, visit the slurm webpage:[https://slurm.schedmd.com/quickstart.html](https://slurm.schedmd.com/quickstart.html)

For the commonly used Slurm commands on the Lawrence HPC, we have provided quick-start documentation with examples within the Wiki.

# Interactive Jobs

##### General Compute

Interactive sessions on compute nodes can be used with the Slurm command "srun". For the use of one node, this command can be used generally as demonstrated below:

```
[user.name@usd.local@login ~]$ srun --pty bash
[user.name@usd.local@node37 ~]$
```

##### HiMem

The Lawrence high-memory \(himem\) partition has two nodes, each with 1.5 TB of RAM. This node is especially useful for jobs requiring a large amount of memory and can be accessed either interactively or with a batch script.

For interactive jobs on the Lawrence himem nodes, use the srun command as follows:

```
[user.name@usd.local@login ~]$ srun --pty -p himem bash
[user.name@usd.local@himem02 ~]$
```

##### GPU

The GPU node must be specifically requested using the “--gres” parameter. GPU access is controlled by cgroups, which means the resource must be requested if it is to be used. This prevents use conflicts. The format for requesting the GPU node \(as specified in the contig file\) is TYPE:LABEL:NUMBER.

TYPE will be “gpu”.

LABEL is defined as “pascal” for the GPU node.

NUMBER is the amount of resources requested. For the GPU node, there are two logic units, so a user can request “1” or “2”.

An example command would be as follows:

```
srun --pty -p gpu --gres=gpu:pascal:1 bash
```

To see which GPUs are available use the following command:

```
nvidia-smi
```

For interactive GPU sessions, the gpu node is requested as below:

```
[user.name@usd.local@login ~]$ srun --pty -p gpu --gres=gpu:pascal:1 bash
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

To use a high memory node within a batch job, add “--partition=himem” to your script.

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

Below is an example batch script which calls the GPU node, this template can be followed when requesting a GPU node on Lawrence:

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

##### **General Compute**

The example below demonstrates how to start a VNC session on a general purpose compute node:

```
[user.name@usd.local@login ~]$ # The vncpasswd command only needs to be run once
[user.name@usd.local@login ~]$ vncpasswd
Password:
Verify:
[user.name@usd.local@login ~]$ sbatch /opt/examples/gui-job.sh
Submitted batch job 2965
[user.name@usd.local@login ~]$ touch job-2965.out
[user.name@usd.local@login ~]$ tail -f job-2965.out
job execution at: Fri Mar 9 12:30:35 CST 2018
running on node node41
using default VNC server /usr/bin/vncserver
got VNC display :2
local (compute node) VNC port is 5902
got login node VNC port 50041
Created reverse ports on login node.]

====================================================

Your VNC server is now running!
To connect:
1) Mac/Linux/MobaXterm users: run the following command FROM A NEW LOCAL TERMINAL WINDOW (not this one)
ssh -L50041:localhost:50041 user.name@usd.local@lawrence.usd.edu
For other users (PuTTY, etc) create a new SSH session and tunnel port 50041 to localhost:50041

2) Then from your computer use a vnc client like TigerVNC Viewer to connect to localhost:50041
You can download TigerVNC Viewer from https://bintray.com/tigervnc/stable/tigervnc
Stopping VNC server
Killing Xvnc process ID 313303
job 2965 execution finished at: Fri Mar 9 12:31:23 CST 2018
Type ctrl-C to return to your terminal session.
^C
[user.name@usd.local@login ~]$

### Output file is job-xxx.out
```

##### HiMem

To request a VNC session on the HiMem node, use the same commands as given under General Compute excepting the following command with sbatch:

```
[user.name@usd.local@login ~]$ sbatch -p himem /opt/examples/gui-job.sh
```

##### GPU

To request a VNC session on the HiMem node, use the same commands as given under General Compute excepting the following command with sbatch:

```
[user.name@usd.local@login ~]$ sbatch --gres=gpu:pascal:1 -p gpu /opt/examples/gui-job.sh
```

##### Viz

The Lawrence viz node is designed for users who wish to do advanced visualization. The viz node gives users access to accelerated 3D graphics \(one node with one GPU having a GTX logic unit\). A typical use case for the viz node is a virtual network computing \(VNC\) job coupled with a real-time graphical user interface \(GUI\). Please note that a graphical job can be run on any node on the cluster and is not solely limited to the viz node \(although the viz node will often have the best performance\).

Viz nodes must be specifically requested using the “--gres” parameter. Viz access is controlled by cgroups, which means the resource must be requested if it is to be used. This prevents use conflicts. The format for requesting the GPU node \(as specified in the contig file\) is TYPE:LABEL:NUMBER.

TYPE will be “vis”.

LABEL is defined as “gtx” for the viz node.

NUMBER is the amount of resources requested. For the Vis node the only option is “1” as there is only one.

To request a VNC session on the HiMem node, use the same commands as given under General Compute excepting the following command with sbatch:

```
[user.name@usd.local@login ~]$ sbatch --gres=gpu:gtx -p viz /opt/examples/gui-job.sh
```

## Partitions

There are two slurm partitions to be aware of when submitting jobs on Lawrence, the default partition \(nodes\) and the preemptible partition. For an in-depth overview of slurm preemption, please visit the corresponding slurm [webpage](https://slurm.schedmd.com/preempt.html).

##### Nodes \(default\) Partition

The default slurm partition is called “nodes” and will run a job for up to two days on a general compute node/s. When running the sbatch or srun command without passing " -p preemptible" or "--partition preemptible", your job will be scheduled on the “nodes” partition.

##### Preemptible Partition

To accomodate longer running jobs, users also have the option of using the preemptible partition \(using the "-p preemptible" or --partition preemptible" flag\). This partition will allow a job to run for up to 90 days on a general compute node/s. However, if the general compute node/s is needed for a new job in the "nodes" partition, the preemptible job will be canceled \(preempted\) to allow the regular job to run.



