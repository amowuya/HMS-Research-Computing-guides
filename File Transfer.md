# File Transfer
[complete guide](https://wiki.rc.hms.harvard.edu/display/O2/File+Transfer)  

## Tools for Copying
### Graphical tools
==FileZila is a standalone sftp tool.==

### Command line tools
`scp`, `sftp`, `rsync` are automatically installed on Mac and Linux.  

## How to copy
Connection paramters:  

* host: `transfer.rc.hms.harvard.edu`
* port: 22 (the SCP/SFTP port)
* username: `jc604` (ecommons ID)
* password: `<ecommons password>`

Make sure to transfer for `/n/groups` or `/n/dataX`, not `/home`.  

Example command to transfer from Mac:

	scp myfile my_o2_id@transfer.rc.hms.harvard.edu:/n/groups/lab/dir1/

