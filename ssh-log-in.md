# How to connect to the HPC using SSH

To start you will need to open a terminal or command line interface. If you are using MobaXterm, use that. Otherwise open your terminal \(Linux, Mac\).

> In MobaXterm \(assuming that you've completed the installation\), click the button 'Start Local Terminal' in order to get to the command line.

Next, you will need to login via an ssh session through the login node.  
You must be given access by the HPC administrator \(which can be requested by contacting the HelpDesk\). Login as so:

```
[userlocal ~]$
[userlocal ~]$ ssh User.Name@hpc.usd.edu
```

> Note: use hpc.usd.edu, not coyotes.usd.edu

You will then be prompted for a password. Enter you regular USD credentials. If you have more than five failed attempts at logging in you will be locked out for one hour or until access is reinstated by the system administrator.

> The password you type will not show up on the screen.

```
User.Name@hpc.usd.edu's password:
```

Once logged in successfully, all users should get the following message:

```
Last login: 
Welcome to hpc.usd.edu, 
The University of South Dakota's High-Performance Computing cluster

Documentation:
http://rcg.usd.edu

***NOTE***
* USER HOME DIRECTORIES ARE NOT BACKED UP
* Computations should not be run directly on this login system.  
* Computational jobs running on this login system will be terminated without warning.    
* Publications resulting from the use of this resource should acknowledge: "Computations supporting this project were performed on High-Performance Computing systems at the University of South Dakota."
* Research Computing staff assisting in the project in any way should be acknowledged. For example: "Research Computing Manager Doug Jennewein provided valuable technical expertise to this project."

If you have any questions, please contact the Help Desk. 
ITS Help Desk
Academic Commons - I.D. Weeks Room 104 
Submit requests online at http://www.usd.edu/ithelp. 
Helpdesk@usd.edu 
Toll Free:  877-225-0027 
Phone: 605-658-6000
```

You will also get the command line prompt on the HPC system.

```
[user@login-0-0 ~]$
```

---



