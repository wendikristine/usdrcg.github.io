# Logging in to an interactive session - qlogin

To start an interactive session on a compute node use the`qlogin` command. This is useful for menu-driven applications or other interactive programs.

By default qlogin will request 1GB of memory, 1 CPU core, and 1GB of scratch disk.

The qlogin command can also request a specific number of CPU cores, RAM, or scratch disk space \(non-shared, local disk available available in /scratch on each compute node\) for your interactive session. For example, the following command requests 4 CPU cores, 24GB of RAM, and 10GB of scratch disk:

`qlogin -pe threaded 4 -l scratch_free=10G,mem_free=24G`

If you only wish to request 24GB of ram, use:`qlogin -l mem_free=24G`

To exit your interactive session type`logout`.



