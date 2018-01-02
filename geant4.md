# PAUP

Paup 4 is available to all users on the cluster. Interactive paup jobs can be run from a qlogin session, and batch jobs may be submitted with the runpaup and runpauprat commands. Batch jobs will continue to run even if you log out. The paup, runpaup, and runpauprat commands are available in the PATH by default.

```
runpaup

```

PAUP \(Phylogenetic Analysis Using Parsimony\) uses NEX files as input. Example files can be found at /share/apps/paup/Sample\_NEXUS\_data/. To run PAUP on a nexus file called myfile.nex, type:

```
runpaup myfile.nex
runpauprat

```

The cluster also provides the runpauprat command for submitting PAUPRat jobs. PAUPRat is a tool to implement Parsimony and Likelihood Ratchet searches using PAUP. To launch a batch PAUPRat job with an input file called myfile.nex, type:

```
runpauprat myfile.nex
```



