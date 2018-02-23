# Lawrence SSH Login for Linux and Mac

To start you will need to open a terminal or command line interface.

Next, you will need to login via an ssh session through the login node. You must be given access by the HPC administrator \(which can be requested by contacting the HelpDesk\). Login as so:

```
[user@localhost ~]$
[user@localhost ~]$ ssh User.Name@lawrence.usd.edu
```

You will then be prompted for a password. Enter you regular USD credentials. \(Note: the password you type will not show up on the screen.\) If you have more than five failed attempts at logging in you will be locked out for one hour or until access is reinstated by the system administrator.

```
User.Name@hpc.usd.edu's password:
```

The password you type will not show up on the screen. Once logged in successfully, all users should get their last login and a command line prompt:

```
Last login: (date and address here)
[user.name@usd.local@login ~]$
```

# Lawrence SSH Login for Windows

Utilization of the Lawrence cluster by WIndows users requires the use of the MobaXterm terminal. MobaXterm can be freely downloaded here \(use the Home Installer Edition\):

[https://mobaxterm.mobatek.net/download.html](https://mobaxterm.mobatek.net/download.html)

Once downloaded, you will open the Moba terminal and the command line prompt will appear:

```
[2017-12-25 19:55.00]  ~
[User.Name.NI11018] ➤
```

You can then ssh onto the Lawrence cluster \(same command as Linux/Mac\). You will be prompted for a password which is your USD credentials \(Note: the password will not show when typing. If the user has more than three tries they will be locked out until an admin override or the lockout expires\)

```
[User.Name.NI11018] ➤ ssh User.Name@lawrence.usd.edu
User.Name@lawrence.usd.edu's password:
Last login: Mon Dec 25 19:37:34 2017 from ni11018.usd.local
[user.name@usd.local@login ~]$
```

You will be given a prompt to begin typing commands. All login goes by default to the login node. Do not run compute jobs on the login node! Please read further instructions on how to use Slurm, the Lawrence cluster workload manager.

