# rclone: Configuration and usage for Google Drive

This software syncs your HPC directory with many popular cloud storage services. Here we will cover instructions for Google Drive.

---

## Set-up and Configuration

First, we need to add rclone to your path. You can also check to make sure you're sourcing the correct file using the `which` command.

```
 [Wendi.Sapp@login-0-0 ~]$ source /share/apps/rclone/env.sh
 [Wendi.Sapp@login-0-0 ~]$ which rclone
 /share/apps/rclone/rclone
```

If you wish to have a separate directory which will contain your Google Drive, make it and navigate there before continuing. For example:

```
[Wendi.Sapp@login-0-0 ~]$ mkdir rclone_GoogleDrive
[Wendi.Sapp@login-0-0 ~]$ cd rclone_GoogleDrive/
```

Next, run the rclone configuration. A prompt will notify you that no remote connections exist. To set up a new connection, type _n_.

```
[Wendi.Sapp@login-0-0 rclone_GoogleDrive]$ rclone config
2017/04/09 18:08:27 NOTICE: Config file "/home/Wendi.Sapp/.config/rclone/rclone.conf" not found - using defaults
No remotes found - make a new one
n) New remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
n/r/c/s/q
>
 n
```

It will prompt you to enter a name. Enter the name, in this case, _remote_.

```
name
>
 remote
```

A lot of information will populate the screen. The first will be a list of available services. In this section, we will choose \#7, Google Drive.

```
Type of storage to configure.
Choose a number from below, or type in your own value
 1 / Amazon Drive
   \ "amazon cloud drive"
 2 / Amazon S3 (also Dreamhost, Ceph, Minio)
   \ "s3"
 3 / Backblaze B2
   \ "b2"
 4 / Dropbox
   \ "dropbox"
 5 / Encrypt/Decrypt a remote
   \ "crypt"
 6 / Google Cloud Storage (this is not Google Drive)
   \ "google cloud storage"
 7 / Google Drive
   \ "drive"
 8 / Hubic
   \ "hubic"
 9 / Local Disk
   \ "local"
10 / Microsoft OneDrive
   \ "onedrive"
11 / Openstack Swift (Rackspace Cloud Files, Memset Memstore, OVH)
   \ "swift"
12 / SSH/SFTP Connection
   \ "sftp"
13 / Yandex Disk
   \ "yandex"
Storage
>
 7
```

The next two prompts will need to be left blank. Simply press Enter to move to the next.

```
Google Application Client Id - leave blank normally.
client_id
>

Google Application Client Secret - leave blank normally.
client_secret
>
```

The next step will ask if you would like to use an autoconfiguration. Since we access the HPC remotely, we must manually connect. Therefore, type _n_.

```
Remote config
Use auto config?
 * Say Y if not sure
 * Say N if you are working on a remote or headless machine or Y didn't work
y) Yes
n) No
y/n
>
 n
```

The configuration will provide a web address for you to copy and paste into your browser. A browser window may automatically appear.

```
If your browser doesn't open automatically go to the following link: https://accounts.google.com/o/oauth2/auth?client_id=20224.apps.googleusercontent.com
&
redirect_uri=urn%33Aoauth%3A2.0%3Aoob
&
response_type=code
&
scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fdrive
&
state=e3e26d91623cce1977b57109
Log in and authorize rclone for access
```

In the browser window, either select the Google account you wish to use or sign into one.

Google will ask if you'd like to provide account access to rclone. Select _Allow_. Then, it will give you a code to copy and paste into your terminal window.

```
Enter verification code
>
 4/iBdkaFE_TQVDw1TdCKD1g1f4w7LHyrUYOj0nQ
```

Your terminal will ask you to verify your actions. If there are no errors, type _y_.

```
--------------------
[remote]
client_id =
client_secret =
token = {"access_token":"ya29.GlsoBJR8t-nYjipMBY40mg0NcNPy09Gr0bJ0fpJmjPaZHWkNgrzeQoVkf5YxUabwETj-R9sBhEm-WX_HvAbrjQYZr-
TokvlhSWYmFM34Gxx7HBy3d_coyTcZsgEz","token_type":"Bearer","refresh_token":"1/HUvQRFACa8H1mkZscYUeEkhrQvTXxsHH_XF67aRQ-ak","expiry":"2017-04-09T19:41:04.517496-05:00"}
--------------------
y) Yes this is OK
e) Edit this remote
d) Delete this remote
y/e/d
>
 y
```

Finally, we'll need to exit the set-up. Do so by typing _q_.

```
Current remotes:

Name                 Type
====                 ====
remote               drive

e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q
>
 q
```

You have completed the set-up for Google Drive.

---

## Usage

In this section, we'll cover a few basic commands to get your HPC directories and Google Drive folders synced.

First, you can list files and directories in the remote drive \(Google Drive\). In this command, you start by using the rclone command, followed by the list command. Then, the name of the remote service is needed, here the name is_remote_. After the name, include a colon and then the path \(folder\). The following is the standard format, followed by an example.

```
rclone ls remote:path
rclone ls remote:Miscellaneous/Scripts/
```

Similarly, you can list the directories in your cloud storage.

```
 rclone lsd remote:path
```

If you'd like to sync two folders \(one on HPC and one on Google Drive\), you can use the following command:

`rclone sync source:path destination:path`

> If dest:path doesn’t exist, it is created and the source:path contents go there.



