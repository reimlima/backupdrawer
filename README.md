# backupdrawer
--------------------------------------------------------------------------------

Client backup script with tar and rsync

# Notice
--------------------------------------------------------------------------------

This script was tested and work well in:

### Linux
* OS Distribution: CentOS release 6.6 (Final)
* Kernel: 2.6.32-504.3.3.el6.x86_64
* GNU bash: version 4.1.2(1)-release (x86_64-redhat-linux-gnu)

# Before use it
--------------------------------------------------------------------------------

Make sure you have a Remote Rsync Server running a daemon.
For more informations, please visit [Rsync] configuration page.

# IMPORTANT WARNING
--------------------------------------------------------------------------------

Don't use this script with files that are currently open to write by another process.

This scenery creates a wrong 'exit status' and makes the script exit without finish all steps. 

# Changelog
--------------------------------------------------------------------------------
* **13/04/2015 - v1**
First Stable Release
* **22/04/2015 - v2**
Added 'old files purge' function
* **08/05/2015 - v2.2**
Some Bug Fixes
* **11/05/2015 - v2.3**
Allow wildcard in 'BKPDIRNFILES' in the conf file.
* **15/05/2015 - v2.4**
added "--ignore-failed-read" option to not exit with nonzero on unreadable files.
* **01/07/2015 - v2.5**
Fixing "testBackupTarFile" function Bug.
* **11/04/2016 - v2.6**
Added option to stop storing local files.
* **05/07/2016 - v2.6.1**
Logrotate file for backupdrawer.
* **05/09/2016 - v2.6.2**
Minor update in BKPFILELOCALCOPY var verification.
* **05/17/2017 - v2.7**
Removing unused conditional in restore function.
Validation for BDAGENTLOG and DESTINATIONTAR directories to exist.
Test if Remote Server exist and if it is listen in rsync port.
Refining some inconsistencies.
* **01/09/2018 - v2.7.1** 
Minor fix when remove old local files. 

# How to use it
--------------------------------------------------------------------------------

CONF FILE:

Just  fill the configuration file with the values for BKPFILENAME, BKPDIRNFILES,
DESTINATIONTAR,  BKPFILERETENTION,  BKPFILELOCALCOPY,  BDAGENTLOG,  SERVERBKP,
SERVERBKPUSER, SERVERBKPPATH, then run the script.

| Legend | Description |
|--|--|
| BKPFILENAME | Little part of backup file name, full name will contain also Hostname and date with hour |
| BKPDIRNFILES | List of directories and files for backup, NONE SLASH '/' in the beginning neither in the end of each element |
| DESTINATIONTAR | Destination path to the backup file |
| BKPFILERETENTION | Time in days to keep a local copy |
| BKPFILELOCALCOPY | Keep a local copy of backup file. "0" to "yes", "1" to "no". Anything else will be ignored |
| BDAGENTLOG | Log path and file |
| SERVERBKP | Remote Server to send the backup file |
| SERVERBKPUSER | Remote Server user access |
| SERVERBKPPATH | Remote Server destination path, must be the same in "/etc/rsyncd.conf" (Read Examples in [Rsync] Doc) |

Example:

```sh
	BKPFILENAME="EtcAndUsr"
	BKPDIRNFILES="etc/cups/printers.conf usr/local/bin"
	DESTINATIONTAR="/var/bdagent"
	BKPFILERETENTION="0"
	BKPFILELOCALCOPY="0"
	BDAGENTLOG="/var/log/backupdrawer/bdagent.log"
	SERVERBKP="faraway.com"
	SERVERBKPUSER="rsync"
	SERVERBKPPATH="backupdir"
```

Is possible to create dynamic configurations with subshell, for example:

- Files wich was rotated with the date from one day ago.
```sh
	BKPDIRNFILES="etc usr/local/bin var/log/nginx/*$(date +%Y%m%d -d "yesterday")*"
```
Daily 'backup directories' in the destination server that will be created automatically.
```sh
	SERVERBKPPATH="backupdir/$hostname/$(date +%Y-%m-%d-%H)"
```

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [Rsync]: <https://download.samba.org/pub/rsync/rsyncd.conf.html>
