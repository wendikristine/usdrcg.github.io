# X11 Forwarding

## Using graphical interfaces? Use X11 Forwarding

In order to use graphical interfaces on the HPC, you'll need to enable X11 forwarding.

### Windows

If you're using MobaXterm, there is no need to change the settings in the software. Simply log in and include a -X option.

```
ssh -X User.Name@hpc.usd.edu
```

### Mac and Linux

The terminal includes X11 forwarding. Type the following:

```
ssh -X User.Name@hpc.usd.edu
```



