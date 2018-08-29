# Personal Perl Packages

author: Josh Cook  
date: 2018-08-29  

**[link to the full guide](https://wiki.rc.hms.harvard.edu/display/O2/Personal+Perl+Packages)**


## Turning on `local::lib`

The `local::lib` Perl module lets you install packages in a directory called "perl5-O2" in your home directory. The following three commands will modify your `.bashrc` file to always look in your local directory first (this need only be done once ever):

```bash
echo 'module load gcc/6.2.0' >> ~/.bashrc
echo 'module load perl/5.24.0' >> ~/.bashrc
echo '[ $SHLVL -eq 1 ] && eval $(perl -I$HOME/perl5-O2/lib/perl5 -Mlocal::lib=~/perl5-O2)' >> ~/.bashrc
```

## Using `local::lib`

Once you've turned it on, installing Perl modules with tools like [`cpan` or `cpanm`](http://www.cpan.org/modules/INSTALL.html) will automatically install them to your local "perl5-O2" directory.

