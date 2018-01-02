# Gaussian and GaussView

### At-a-Glance

| Item | Information |
| :--- | :--- |
| Description | Computational chemistry software with  graphical user interface \(GaussView\). |
| Command: GaussView | `gv file_name_optional`\(requires[X11 forwarding](https://github.com/USDRCG/usdrcg.github.io/wiki/X11-Forwarding)\) |
| Command: Gaussian | `rungaussian file_name` |

---

## User Guide

Gaussian 09 is available on the HPC cluster. To run Gaussian, your account must be a member of the Gaussian group.

When you log in, type the following:

```
module load gaussian-09
```

The above line may be included in \(for example\) your &gt; .bashrc file if you do not wish to type it each time you log in.

After this the g09 command should be present in your PATH environment variable, the g09root environment variable should be set, and`$g09root/g09/bsd/g09.profile`should automatically be sourced. The`g09.sh`script also sets GAUSS\_SCRDIR to '/scratch/yourusername', creating it if necessary.

To run Gaussian directly, for example from a`qlogin`session, type`g09 < input-file-name`. However, it is recommended that you launch your Gaussian jobs via the job scheduler, either with the`rungaussian`command or by writing your own job submission script.

### The`rungaussian`command

The simplest way to run a Gaussian job is to use the`rungaussian`command. To run Gaussian on the file `myinput.com`, type the following from the directory containing `myinput.com`.

```
rungaussian myinput.com
```

> Notes:
>
> * Standard output is written to the file`Gaussian-USERNAME-JOBID.out`, and errors are written to`Gaussian-USERNAME-JOBID.err`.
>
> * GAUSS\_SCRDIR is set to `/scratch/yourusername/JOBID`.
>
> * Scratch disk may be requested after the input file name with -s, `rungaussian myinput.com -s 10G`
>
> * If no scratch disk is specified, 1GB is used.
>
> * Your Gaussian input file should contain a `%NProcShared` line requesting a specific number of processors.
>
> * It should also contain a `%Mem` line requesting a specific amount of memory \(100MB, 2GB, etc\).
>
> * If the number of processors is not specified 1 processor is used.
>
> * If memory is not specified 1GB is used.
>
> * No more than 8 processors and 31GB memory may be requested by a single Gaussian job.
>
> * Scratch disk may be specified with -s
>
> * A Gaussian input file requesting 4 processors and 2.5 GB of memory would contain the following two lines:
>
>   `%NProcShared=4`
>
>   `%Mem=2.5GB`

### Writing your own job submission script

Advanced users may wish to run Gaussian with their own job submission script. When writing your own scripts to submit multi-processor Gaussian jobs, your script should request processors from the “smp” parallel environment to ensure all processors are provisioned from a single compute node. For example, to request 4 processors, include a line like the following in your job script:

```
#$ -pe smp 4
```

Your script should also request memory from the job scheduler by including`-l mem_free=X`where X is the amount of memory you wish to request for your job \(500M, 2G, etc\). Note that while Gaussian’s %Mem specifies the amount of memory for the entire job, mem\_free specifies the amount of memory per processor \(see below\).

The number of processors requested in your job script should match the amount specified by %NProcShared in your input file. The amount of memory requested by %Mem in your input file should be equal to the amount requested with mem\_free times the number of processors requested. For example, a job submission script for a 4-processor job requesting a total of 4GB memory would contain the following two lines:

```
#$ -pe smp 4
#$ -l mem_free=1G
```

And the corresponding lines in the Gaussian input file would be

```
%NProcShared=4
%Mem=4GB
```

Similarly, you can request scratch disk with`-l scratch_free`. The following example requests 10GB of scratch disk:

```
#$ -l scratch_free=10G
```

### Customizing the Scratch Directory, GAUSS\_SCRDIR

By default, the Gaussian scratch directory resides on local disk in the /scratch directory. If your gaussian jobs’ RWF files are filling up the /scratch/ directory, a possible workaround may be to use the %RWF command in your Gaussian input file. The %RWF command allows you to provide a specific location for Gaussian’s read-write, and you can pass it the name of a directory in your home directory \(eg `%RWF=/home/jsmith/gaussian/rwf`\). User home directories have much larger capacity than local disk, and in our experience writing a single large file such as Gaussian’s RWF file to this location should be at least as fast as writing to local disk.

---

## GaussView

### Running GaussView

To run GaussView you must connect to the cluster with “X11 Forwarding” enabled in your SSH client. On Mac and Linux this means connecting with “ssh -X” instead of just “ssh”. See [X11 Forwarding](https://github.com/USDRCG/usdrcg.github.io/wiki/X11-Forwarding)for more information.

Once logged in, type

```
source /share/apps/g09/g09.sh
```

and then type

```
gv
```

The GaussView window should display on your screen.

### Launching Gaussian from GaussView

To avoid overwhelming the login machine, GaussView should run Gaussian only via the`rungaussian`command. To configure GaussView to launch Gaussian via the`rungaussian`command do the following \(this only needs to be done once\):

1. From GaussView, select File-&gt;Preferenes. The GaussView Preferences screen is displayed.

2. Select Job Setup on the left.

3. Select “Execute using custom command line”

4. In the Command Line box, delete and existing text and type

   ```
    rungaussian @INFILE
   ```

The GaussView Preferences screen should now look like this:

![](https://camo.githubusercontent.com/f8c7e8d4d90dd0a41d03f9d184a94b2745acfc5c/687474703a2f2f7573647263672e6769746875622e696f2f6173736574732f696d672f4761757373566965776a6f6273657475702e706e67 "GaussView Set-Up")

1. Click OK

> Notes:
>
> * When you launch Gaussian, GaussView will immediately display the following message:
>
> ![](https://camo.githubusercontent.com/1a794d567fe61c9959bcb2e8bc941d51983d8bb3/687474703a2f2f7573647263672e6769746875622e696f2f6173736574732f696d672f476175737369616e4a6f627465726d696e617465642e706e67 "GaussView Error")
>
> * This is because GaussView doesn’t know that Gaussian has been launched on a compute node instead of the login node where GaussView is running.
> * The GaussView job manager \(under Calculate-Current Jobs\) will not report on any launched jobs. Your Gaussian job will be managed by the job scheduler in the same manner as your regular Gaussian jobs. You can see your Gaussian job’s job ID and monitor its execution with
>   `qstat`
>   and cancel it with
>   `qdel`
>   .



