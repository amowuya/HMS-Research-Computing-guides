# File Transfer
[complete guide](https://wiki.rc.hms.harvard.edu/display/O2/File+Transfer)  

## Tools for Copying
### Graphical tools
[**FileZila**](https://filezilla-project.org) is a standalone sftp tool for Mac, Linux, and Windows. I recommend using it for simple movement of files if you are not comfortable with the command line (Linux/UNIX).

### Command line tools
`scp`, `sftp`, `rsync` are automatically installed on Mac and Linux.  

## How to copy
Connection paramters for **FileZilla**:  

* host: `transfer.rc.hms.harvard.edu`
* port: 22 (the SCP/SFTP port)
* username: `<ecommons ID>` (ecommons ID)
* password: `<ecommons password>`

Make sure to transfer large files to `/n/groups/...` or `/n/dataX/...`, not `/home/<ecommons ID/...` (where there is only 100 GB allowed).  

Example command to copy from Mac using `scp`:

```bash
scp myfile <ecommons ID>@transfer.rc.hms.harvard.edu:/n/data2/bidmc/medicine/haigis/
scp -r myfolder <ecommons ID>@transfer.rc.hms.harvard.edu:/n/data2/bidmc/medicine/haigis/
```

Notice the necessity for the `-r` flag when moving/copying entire directories.  

To setup SFTP, use the following command:

```bash
sftp <ecommons ID>@transfer.rc.hms.harvard.edu
```
where you will then be asked to input your password. This will bring you to a command line where you can copy files to and from using the `put` and `get` commands. This is essentially a command line version of FileZilla, so I would only recommend using this if you are comfortable with the command line or FileZilla does not work on your opterating system.