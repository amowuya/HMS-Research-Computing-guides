# How to choose a partition in O2

author: Josh Cook  
date: 2018-06-13  

[link to full guide](https://wiki.rc.hms.harvard.edu/display/O2/How+to+choose+a+partition+in+O2)


![partition_flowchart]()

Any partition can be used to request an interactive session; the interactive partition has a dedicated set of nodes and higher priority.  

Any partition can run single or multi-core jobs. More information is available for multi-core jobs at the dedicated [page](https://wiki.rc.hms.harvard.edu:8443/display/O2/How+To+Submit+Parallel+Jobs+in+O2). This can also be accomplished using multiple chained `srun` commands:

	#/bin/bash
	#SBATCH -c 8
	#SBATCH --mem 32G
	srun -c 2 --mem=8G COMMAND1 & 
	srun -c 4 --mem=8G COMMAND2 & 
	srun -c 1 --mem=4G COMMAND3 & 
	srun -c 1 --mem 12G COMMAND4 & 
	wait
	
Also, some software (especially alignment tools!) can run multi-core processess using a specific flag. Below is an example on [Bowtie2](link_to_full_doc)



TODO: add links for flowchart image and Bowtie2 documentation page.
TODO: add example of Bowtie command for multi-core
TODO: add table of the different partitions (maybe before the flowchart?)