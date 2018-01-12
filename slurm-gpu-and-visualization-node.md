# Slurm for GPU and Visualization Node

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



