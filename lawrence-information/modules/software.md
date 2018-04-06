edit metadata

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

  


