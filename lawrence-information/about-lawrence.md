# About Lawrence

The Lawrence Supercomputer was acquired through a combination of state and federal funding: a FY16 SD Board of Regents Research And Development Innovation award, and National Science Foundation Major Research Instrumentation award [OAC-1626516](https://nsf.gov/awardsearch/showAward?AWD_ID=1626516&HistoricalAwards=false).

Lawrence runs the CentOS Linux operating system and is made up of over 2,000 CPU cores, including systems with 1.5TB of memory, GPU accelerators, and over 400TB of shared high-speed data storage accessible via a 56Gb FDR Infiniband network. Lawrence has an estimated performance of over 60TFLOPS.

The hardware specifications for Lawrence vary by node and are as follows:

**node01-node80**

80x general compute nodes

dual 12-core SkyLake 5000 series CPUs

96GB RAM

240GB SSD

**gpu01**

1x GPU Node

dual 12-core SkyLake 5000 series CPUs

1926GB RAM

240GB SSD

2x Nvidia Tesla P100 16GB GPUs

**viz01**

1x Viz Node

dual 12-core SkyLake 5000 series CPUs

192GB RAM

240GB SSD

Nvidia GTX 1080i 11GB graphics adapter

**himem01, himem02**

2x Large Memory Node

dual 14-core SkyLake 5000 series CPUs

1.5TB RAM

2x 240GB SSD, mirrored

**login**

1x Login Node

dual 12-core SkyLake 5000 series CPUs

96GB RAM

2x 240GB SSD, mirrored

**head**

1x Management node

dual 12-core SkyLake 5000 series CPUs

96GB RAM

2x 240GB SSD, mirrored

**zfs01, zfs02**

2x ZFS Storage nodes, 432TB Raw total

RAIDZ2 across the 2x 216TB storage nodes

FDR IB, 5:1 oversubscription

1Gb Ethernet in-band management network

1Gb Ethernet out-of-band management network

