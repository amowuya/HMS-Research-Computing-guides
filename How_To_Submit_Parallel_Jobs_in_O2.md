# How To Submit Parallel Jobs in O2

author: Josh Cook  
date: 2018-06-14  
[link to the full guide](https://wiki.rc.hms.harvard.edu:8443/display/O2/How+To+Submit+Parallel+Jobs+in+O2#HowToSubmitParallelJobsinO2-DistributedMemoryParallelization)  

**_Very Important_: Submitting a parallel job will not make that job run parallel unless the application you are running explicitly supports parallel execution.**

O2 supports:

* shared memory parallelization on a single node, typically multithread, such as [OpenMP](http://www.openmp.org/)
* distributed memory parallelization across multiple nodes, typically multitask such as MPI 
* a combination of the two

## Shared Memory Parallelization

### Background

Many standard applications now have flags to run multithreaded: use multiple cores on a node, but all use the same memory. The most common type of multithread application uses the [OpenMP](http://www.openmp.org) application programming interface.

### Running jobs

To submit a job that uses multiple cores, you must specify the number of job cores you want to use with the sbatch flag `-c <Ncores>`. *The maximum number of cores that can be requested is 20.*

Below is an example job requesting a maximum of 24 hours to run the application `your_multithreaded_application` using 4 cores and 10 GB of memory:

```bash
sbatch -p medium -t 24:00:00 -c 4 --mem=10G --wrap="your_multithreaded_application"
```

Note that each application may have a different way of specifying the number of threads to execute. Please see the documentation for the appropriate flag, (often for a number of _cores_, _nodes_, _cpus_, or _threads_). You can also ask Research Computing for help with a particular application.  

Below is an example of running two commands in parallel by requesting multiple cores with the `-c <Ncores>` flag and using the `&` symbol to connect jobs capped with `wait`[^1]:

[^1]: The `wait` command ensures that all applications started in parallel have completed.

```bash
sbatch -p short -t 4:00:00 -c 2 --wrap="application_1 & application_2; wait"
```

Note: This type of parallel job can be submitted to any partition except mpi.

## Distributed Memory Parallelization

### Background

Some programs allow "distributed memory parallelization. This option is used for multitask applications capable of running in parallel over a distributed memory system, i.e. the allocated cores are not necessarily on the same node. The different tasks are usually capable of communicating with each other to exchange data, necessary because each task only has access to its own memory. In addition, the parallel tasks in this type of application are usually initiated by a wrapper (i.e. a program that uses calls other programs) that interfaces with the scheduler (Slurm) to know the nodes where the cores were allocated. The most common type of multitask application uses the MPI (Message Passing Interface) method. [OpenMPI](http://www.open-mpi.org) is installed and available on the O2 cluster (see below for more details).

### Preparation

OpenMPI uses `ssh` for inter-node communication. Public and prive keys are required, but already configured[^2]. 

[^2]: The instructions here were rather confusing on what is required of the user, so this may need to be changed after trying it out.

The `gcc/6.2.0` and `openmpi/2.0.1` or `/3.1.0`[^3] modules must be loaded:

```bash
module load gcc/6.2.0
 
module load openmpi/2.0.1
or
module load openmpi/3.1.0
```

[^3]: My naive recommendation is to use version 3.1.0 of OpenMPI unless the documentation for your application specifies 2.0.1.

### Running jobs

You must specify the number of required tasks (i.e. cores) you want using the flas `sbatch -n <nstasks> -p mpi ...` to submit a multitask job. You can request up to 640 cores. (`mpi` jobs can be run on ther other partitions, but are limited to 20 cpus.)  

The following example is used to submit an `mpi` job requesting 64 cores and up to 3 days:

```bash
$ sbatch -n 64 -p mpi -t 3-00:00:00 --wrap="mpirun -np 64 your_mpi_application"
```

or by submitting the following script (using `sbatch myjob.sh`):

```bash
#!/bin/bash
#SBATCH -n 64
#SBATCH -p mpi
#SBATCH -t 3-00:00:00
#SBATCH --mem-per-cpu=4G

mpirun -np 64 your_mpi_application
```

*Note the use of `mpirun` in place of the `sbatch` or `srun` to submit a commpand.*  

A specific number of cores per node can be requested using the flag `--ntasks-per-node`; the following command requests 40 cpu cores over 10 nodes, thus using 4 cpus per node:

```bash
sbatch -n 40 --ntasks-per-node=4 --mem-per-cpu=4000 -p mpi -t 3-00:00:00 --wrap="mpirun -np 40 your_mpi_application"
```

*Note the use of `--mem-per-cpu` flag instead of `--mem` when submitting an MPI job.*

## Combining Distributed and Shared Memory Parallelization

Some applications support a *hybrid parallelization model* where the MPI approach is used to distribute a number of tasks across different nodes and each of these tasks runs as a multithread process. In this scenario the total number of cores used by a job is the product of `Ntasks` X `Nthreads`.  

The following example initiates 10 MPI tasks where each task runs as a multithreaded application using 4 cores (for a total of 40 cores): 

```bash
sbatch -n 10 -c 4 -p mpi -t 3-00:00:00 --wrap="mpirun -np 10 your_mpi+openmpi_application"
```

## More Information

### Table of common software that has parallel processing capbabilities

| Software | Purpose | Comments |
|:---------|:--------|:---------|
| Bowtie2 | sequence alignment | must use the flag `-p` |

(updated: 2018-06-14)