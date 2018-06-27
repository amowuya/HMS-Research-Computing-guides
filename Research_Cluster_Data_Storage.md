# Research Cluster Data Storage
author: Josh Cook  
date: 2018-06-26  

[Link](https://wiki.rc.hms.harvard.edu/display/O2/Research+Cluster+Data+Storage) to the complete wiki

If you haven't yet, it is likely worth first reading the [Filesystems](Filesystems.md) page.  

---

All storage on the HMS Research Computing cluster is **free**.

| Type | Availability | Size Limit | Replication | Retention | Snapshot | Performance |
|:--|:--|:--|:--|:--|:--|:--|:--|
| `/n/scratch2`| everyone | 10 TB | no | 29 days | no | *FAST* |
| `/home` | everyone | 100 GB | yes | indefinite | yes | moderate |
| group directories | groups | varies | yes | indefinite | yes | moderate |
| collaborations | HMS Quad | varies | yes | indefinite | yes | moderate |
|`/tmp` | everyone | small | no | none | no | *FAST* |

__Replication__: data are copied nightly to another location  

__Snapshot__:  each directory contains an invisible, read-only, `.snapshot` directory containing 14 days of daily snapshots, and 60 days of weekly snapshots 

*Note*: only HMS Quad labs can initate a collaboration directory, though off-Quad groups can be added.

## `/n/scratch2/ecommonsID`

This filesystem if for *large, temporary* files (not the best option for many small temporary files). If you are running large pipelines, it is recommended that you write intermediary files here. There are no backups, and files are purged after 30 days of no access. To use scratch2 in a job, you must request it so your job is given to a node with access to the filesystem.

```bash
sbatch --constaint="scratch2"
```


## `/home/ecommonsID`

This is your home directory and is limited to 100 GB. Your home directory is backed-up every night inside `.snapshot` which has 14 days worth of daily snapshots, and 60 days of weekly snapshots. Every night, your /home directory is copied to an off-site location for the following 24 hours.


## group directories

Haigis Lab group directory: `/n/data2/bidmc/medicine/haigis`
Please, make your own folder: `mkdir <name_of_folder>`

Labs may install their own group-specific software and share data here. These are backed up and snapshotted in the same way as `/home`.


## `research.files`

Collaborations created by HMS IT are on the `research.files` filesystem. This filesystem is mostly used for sharing data between labs, or for departmental shared space, and it can be mounted as a shared drive on Windows and Mac desktops. Contact [itservicedesk@hms.harvard.edu](itservicedesk@hms.harvard.edu) with questions about research.files. When needed, this filesystem can be accessed as `/n/files` on a few "transfer compute nodes" (permission is required for access.)

## `/tmp`

This is temporary local storage on a single compute node that offers the fastest performance option. Write temporary intermediate files to the `/tmp` directory. There is not a lot of space, and you will be sharing it with anyone else that requires the use of `/tmp` on that node. **Do not write files you want as output to this directory.**[^1]

[^1]: Each node has a different `/tmp`, and if you need to fetch files from there, you will need to ssh directly to that compute node. Also, these files may be deleted any time after your job finishes.
