# Modules

The Lawrence HPC uses modules for the use of software applications on the HPC. Modules allows various versions of software to be available, and also allows a way to make new software. This document provides a brief overview of module commands as they pertain to USD's Lawrence HPC.

Once you are logged into Lawrence, the module commands will be available to you. Following is a brief overview of the basic module commands:

| _Command_ | _Description_ |
| :--- | :--- |
| module avail | show all modules that are available on the system |
| module load SOME.APP | load the listed applciation \(as long as it is available\) |
| module unload SOME.APP | unload a previosuly loaded module |
| moduel list | list the modeuls you have loaded |
| module help | gives you information regarding the module command |

The following example uses module commands to load R version 3.4.1 and then open R for command line use on Lawrence:

```
[user.name@usd.local@login ~]$ module avail
r/3.4.1
[user.name@usd.local@login ~]$ module load r/3.4.1 
[user.name@usd.local@login ~]$ R

R version 3.4.1 (2017-06-30) -- "Single Candle"
Copyright (C) 2017 The R Foundation for Statistical Computing
Platform: x86_64-pc-linux-gnu (64-bit)

>
```

## Bioconda

Bioconda is a channel software manager of conda which can be used for installing various bioinformatics applcations. Bioconda is recommended for those wishing to install software that is not readily available as a module. More information on using bioconda can be found on the Bioconda documentation page [here](https://bioconda.github.io/). Packages currently available on Bioconda can be found [here](https://bioconda.github.io/recipes.html#recipes).

To install bioconda in your home directory on Lawrence, run the install-bioconda script as follows:

```
[user.name@usd.local@login ~]$ /apps/install-bioconda.sh
Downloading installer
Running installer
PREFIX=/home/usd.local/joseph.madison/anaconda3
Installing...
...
Done!
```

Bioconda will now be available through your home directory to install software.

## Math Libraries

##### Intel Math Kernel Library \(MKL\)

The Intel MKL library is available on Lawrence and is the recommended math library for most applciations. This library is configurable to various compilers and languages. Functions provided by Intel MKL include BLAS, LAPACK, and FFTW. For more information on Intel MKL, please visit the developer documentation [webpage](https://software.intel.com/en-us/mkl/documentation).

Intel also provides a tool to generate appropriate command line options for your particular compiler, integer size, and threading model which can be found [here](https://software.intel.com/en-us/articles/intel-mkl-link-line-advisor).

Example command line options for C and GCC compilers can be found below. These comannds would be added after running "module load intel":

Intel C compiler:

```
-DMKL_ILP64 -I${MKLROOT}/include  -L${MKLROOT}/lib/intel64 -lmkl_intel_ilp64 -lmkl_sequential -lmkl_core -lpthread -lm -ldl
```



GCC C compiler:

```

-DMKL_ILP64 -m64 -I${MKLROOT}/include -L${MKLROOT}/lib/intel64 -Wl,--no-as-needed -lmkl_intel_ilp64 -lmkl_sequential -lmkl_core -lpthread -lm -ldl
```



