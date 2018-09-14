# Local Software Installs

author: Josh Cook  
date: 2018-09-13  

Users can compile and install software in their `/home` directories or shared directories (e.g. `/n/groups` and `/n/dataX`).  

## Quick Start

Download the source files using `wget` or `curl`, unpack the compressed files (eg. `.tar`, `.gz`, etc.), and reading the README or installation guide for further, software-specific instructions. Below is an example session:

```bash
srun --pty -p interactive -t 0-2:00 --mem 10G -c 4 /bin/bash
wget <http://... or ftp://...>
gunzip filename.gz
cd newsoftwarefolder
less README
```

Often, you will need to load modules such as python or perl for the set up.

```bash
module load gcc python/version perl/version
```

A common setup formula is to run the `make` then `make install` commands:

```bash
make
make install
```

You can add executables to your `PATH` using the following command:

```bash
~/newsoftwarefolder$ export PATH=/home/newsoftware
```