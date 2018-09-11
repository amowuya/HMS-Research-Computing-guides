# Personal Python Packages

author: Josh Cook  
date: 2018-09-11  
full guides: 
- [Personal Python Packages](https://wiki.rc.hms.harvard.edu/display/O2/Personal+Python+Packages)
- [Conda on O2](https://wiki.rc.hms.harvard.edu/display/O2/Conda+on+O2)


## Basics

Though many Python packages have been installed for each version of Python, it is still recommended to maintain your own library. Some useful commands:

| Command | Meaning |
|---------|---------|
| `module avail python` | show available versions of Python |
| `module load python/version` | load a specific version of Python |
| `pip freeze` | shows the packages installed for the loaded version of Python |

Before using the above commands, you must have loaded gcc: `module load gcc`


## Using a Virtual Environment

### Setup

On your home directory, use the following commands to set up your virtual environment "yourenvname":

```bash
module load gcc python/version
which virtualenv
virtualenv yourenvname --system-site-packages
```

The `--system-site-packages` flag includes the already installed packages in your library. Exclude it if you do not want this.  

You can create multiple virtual environments and they can be removed using `rm -rf yourenvname`.  

### Basic Usage

Begin by activating the virtual environment:

```bash
source yourenvname/bin/activate
```

Confirm you are in the virtual environment using the commend:
```bash
which python
```
which should return something like `~/yourenvname/bin/python`. You are now within your virtual environment where you can use python like normal. To exit the virtual environment, use the following command:
```bash
deactivate
```

### Installing Packages

Inside of your virtual environment, you can install packages from the command line using `pip`:
```bash
pip install nameofpackage
```


## Using Conda

### Basics

Some common commands:

| Command | Meaning |
|---------|---------|
| `module spider conda` | show available versions of Conda |
| `module load conda2/version` | load a specific version of Conda |
| `conda info --envs` | show available Conda environments |
| `conda create -n yourenvname` | create an environment |
| `source activate yourenvname` | activate an environment |
| `conda-env remove -n yourenvname` | remove an environment |
| `source deactivate` | exit the current environment |
| `conda search nameofpackage` | search for a package |
| `conda install nameofpackage` | install a package |

### Setup

Begin by loading the Conda module:

```bash
module load conda2/version
```

You can see available environments:

```bash
conda info --envs
```

or create an environment:

```bash
conda create -n yourenvname
```

When you are done, exit the environment:

```bash
source deactivate
```

### Installing Packages

From within an environment, you can search for and install a package

```bash
conda search nameofpackage
conda install nameofpackage
```

### Python Version

By default, Conda uses Python 2.7. You can create a Conda environment using Python 3.

```bash
conda create -n yourenvname python=3.6.5
source activate yourenvname
which python
python --version
```

The last two commands above should show you are using the desired version of Python.


