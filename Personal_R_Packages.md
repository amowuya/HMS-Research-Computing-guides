# Personal R Packages

author: Joshua Cook  
date: 2018-07-01 

*Note:* in this guide, replace `VersionSelected` with the version of R you want to use. At the time of writing, the newest version of R is 3.5.1, but the versions available on O2 are 3.2.5, 3.3.3, 3.4.1 (use `module spirder R` on O2 to see the current options).  


## Setting up a personal R library (recommended)

All packages installed by R will be saved here by default. To construct the library, use the following commands: 

```bash
mkdir ~/R-VersionSelected/library
echo 'R_LIBS_USER="~/R-VersionSelected/library"' >  $HOME/.Renviron
export R_LIBS_USER="~/R-VersionSelected/library"
```
__command 1:__ makes a new folder which will become the library (`~` is your home directory)  

__command 2:__ sets this directory as the R environment  

__command 3:__ makes the variable `$R_LIBS_USER` available to other processes[^1]

[^1]: More information on the `export` command can be found [here](https://linuxconfig.org/learning-linux-commands-export)). 

## Starting an Interactive R session

Do *not* execute R from the login node. Instead, start an interactive session:  

```bash
srun --pty -p interactive -t 0-1:00 --mem 10G /bin/bash
module load gcc/6.2.0 R/VersionSelected
R
``` 

Make sure you allocate the necessary amount of memory -- all variables in R are held in memory. Therefore, if you read in a 10 Gb file, it will require at least 10 Gb of memory. (There are more memory efficient mechanisms available in R, such as using HDF5 via the [rhdf5 package](https://www.bioconductor.org/packages/release/bioc/html/rhdf5.html).)  

## Installing packages

Once inside an R session, installing packages is like normal:

For packages hosted on [CRAN](https://cran.r-project.org):

```r
> install.packages("package_name")
> library(package_name)
```

For packages hosted on [GitHub](https://github.com):

```r
> library(devtools)
> install_github('username/repo')
> library(package_name)
```

For packages hosted on [Bioconductor](https://www.bioconductor.org):

```r
> source("http://bioconductor.org/biocLite.R")
> biocLite("package_name")
> library(package_name)
```

