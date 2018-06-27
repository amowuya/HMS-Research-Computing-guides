# Filesystems
author: Josh Cook  
date: 2018-06-12  

[link to the full guide](https://wiki.rc.hms.harvard.edu/display/O2/Filesystems)  

Where to put your files depends on how big they are, who needs to see them, whether they are temporary, and how you will be accessing them.  

## Directories

### Home

Home directory: `/home/ecommonsID`  

100 GB limit on the home directory.  

### Group

Group directory: `/n/data2/bidmc/medicine/haigis/Cook`  

A group directory is used by a lab (or a set of researchers sharing data). These directories can be read by any member of the lab, which is quite useful when multiple researchers need to see the same data. Unlike home directories, the entire lab directory has a quota, and lab members work together to keep the space from filling up. These directories are used for large data sets, reference data, or scripts used by a whole lab.

### Scratch 

Scratch directory: `/n/scatch2/ecommonsID`  

Each user is entitled to 10 TB in the `/n/scratch2` filesystem. You can create your own directories inside `/n/scratch2/` and put data in there. **These files are not backed up and will be deleted if they are not accessed for 30 days.**  

Scratch will not work very well with workflows that write many thousands of small files. It is designed for workflows with medium and large files (> 100 MB). Luckily, many next-gen sequencing analysis, image analysis, and other bioinformatics workflows use large files.

### Temporary filesystems

These filesystems allow fast read and writes, but are not backed up. If you are doing significant I/O on a networked filesystem (like `/n/groups` or `/home`), it is often better to copy files to the temporary filesystem, process them, and copy output back, than to operate directly on files in your home or group directory.  

`/tmp` is the standard UNIX temporary directory. **`/tmp` is a different hard drive on each machine.** A file you place in `/tmp` on a login node is not available in `/tmp` on a compute node or even on a different login node. If a job writes to `/tmp`, it will write to `/tmp` on the node the job is running on. Your job should copy it back to a shared filesystem like `/home`, because it may get deleted from the compute node.  

Temporary filesystems are never backed up and are automatically purged periodically.

## Restoring Backups

Most shared filesystems retain snapshots for up to **60 days**, the exception being temporary filesystems. If snapshots are available for a directory, they are located in a hidden directory called `.snapshot`. (This directory will not be visible by `ls -a`.)  
To retrieve a backup:

* From a command prompt on O2, type `cd .snapshot` to see available backups of that directory.
* Inside the `.snapshot` directory, there will be directories with date/times in their names, containing a copy of all files at that date/time. Each sub-directory will also have its own `.snapshot` directory.
* You can't write files to these directories, but you can copy files from here back to the original directories with the `cp` command.