backupdrawer
--------------------------------------------------------------------------------

Client backup script with tar and rsync

Notice
--------------------------------------------------------------------------------

This script was tested and work well in:

* Linux
        - OS Distribution: CentOS release 6.6 (Final)
        - Kernel: 2.6.32-504.3.3.el6.x86_64
        - GNU bash: version 4.1.2(1)-release (x86_64-redhat-linux-gnu)

BEFORE USE IT:

Make sure you have a Remote Rsync Server running a daemon.

For more informations, please visit this link:

	https://download.samba.org/pub/rsync/rsyncd.conf.html

Changelog
--------------------------------------------------------------------------------

[13/04/2015] - v1   - First Stable Release
[22/04/2015] - v2   - Added 'old files purge' function
[08/04/2015] - v2.2 - Some Bug Fixes

How to use it
--------------------------------------------------------------------------------

CONF FILE:

Just  fill the configuration file with the values for BKPFILENAME, BKPDIRNFILES,
DESTINATIONTAR,  BDAGENTLOG,  SERVERBKP,  SERVERBKPUSER, SERVERBKPPATH, then run
the script.

Legend:

	BKPFILENAME:	Little part of backup file name, full name will contain
			also Hostname and date with hour

	BKPDIRNFILES:	List of directories and files for backup.
			NONE SLASH '/' in the beginning neither in the end of each element

	DESTINATIONTAR:	Destination path to the backup file

	BDAGENTLOG:	Log path and file

	SERVERBKP:	Remote Server to send the backup file

	SERVERBKPUSER:	Remote Server user access

	SERVERBKPPATH:	Remote Server destination path, must be the same in "/etc/rsyncd.conf
			Read Examples in https://download.samba.org/pub/rsync/rsyncd.conf.html

Example:

	BKPFILENAME="EtcAndUsr"
	BKPDIRNFILES="etc/cups/printers.conf usr/local/bin"
	DESTINATIONTAR="/var/bdagent"
	BDAGENTLOG="/var/log/backupdrawer/bdagent.log"
	SERVERBKP="faraway.com"
	SERVERBKPUSER="rsync"
	SERVERBKPPATH="backupdir"
