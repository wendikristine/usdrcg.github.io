# Transferring Files

Transferring files onto and off of your Lawrence home directory can be done using several methods available to researchers at USD. This section will cover the movement of files between local systems and the Lawrence HPC.

### SCP

The standard command line method for file movement between hosts is the `scp`command \(secure copy\). This is an ssh based protocol designed for moving files between local and remote hosts. To get files from your local computer, you will need to open a local terminal session on your computer \(Do not connect to the HPC!, in this example, local@xyz is my local PC\).

```
[local@xyz ~]$
```

The syntax of the `scp` command has four parts: 1. `scp` command, 2. The file you are moving, 3. The path to the file you want to copy, and 4. The target local directory where this file will be downloaded to.

Type the `scp` command as follows \(type the path you want your file transferred to on Lawrence; here I use ''some.folder'\):

```
[local@xyz ~]$ scp file.name user.name@lawrence.usd.edu:/home/user.name/some.folder
user.name@lawrence.usd.edu's password: 
file.name              100% 8893     8.7KB/s   00:00
```

The last line tells you stats on the transfer. You can also use scp for other data transfer applications including HPC to local PC, between HPCs, and between PCs. In a separate terminal where I am logged into Lawrence, I can check that the file was transferred and put into some.file.

```
[Joseph.Madison@login-0-0 some.file]$ ls
file.name
```

### Drag-and-Drop Option

If you like moving files using the drag-and-drop method, this is also possible using MobaXterm or Cyberduck. This next file moving method uses sftp, or SSH \(or Secure\) File Transfer Protocol. For this we will open up MobaXterm or Cyberduck.

**MobaXterm**

In MobaXterm, the file explorer/hierarchy is visible just to the left of the command line interface.

![](/assets/moba_1.png)

From this section of the MobaXterm window, you can drag and drop files between either computer as you desire. 



**Cyberduck**

Cyberduck can also be used for moving files by sftp. You can find the Cyberduck installation [here](https://cyberduck.io/). Once installed, opening Cyberduck should return a window as follows:

![](/assets/cyberduck_1.png)

You will need to open a connection by clicking on the 'Open Connection' icon. This will return a window to fill in with the host information. Fill this window in as shown below \(note user.name will be your persnaol Lawrence username\). Be sure to choose SFTP and port 22:

## ![](/assets/cyberduck_2)

After succesfully connecting, you can upload files into your Lawrence folders on your home directory by dragging and dropping from your desktop, or by clicking the upload icon at the top of the Cyberduck display.

![](/assets/cyberduck_3.png)

