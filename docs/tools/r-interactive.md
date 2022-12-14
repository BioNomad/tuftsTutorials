## R Interactive Session

- Login to the HPC cluster either by Command Line or the OnDemand Website:

!!! info ""

    For information on how to log into the cluster check out:
    
    [Navigate To The Cluster :octicons-info-16: ](../hpc-user-guide/navigate-to-cluster.md){:target="_blank" rel="noopener" .md-button .md-button--primary }

- From the login node, load R module and associated modules

```
module load R/4.0.0 boost/1.63.0-python3 java/1.8.0_60 gsl/2.6
```

- Additional modules may need to be loaded, such as `sf/R_4.0.0` 

- Allocate computing resources. Start an interactive session with your desired number of cores and memory, here we are using 2 cores with 4GB of memory: 

```
srun -p interactive -n 2 --mem=4g --pty bash
```

!!! note
    Interactive partition has a default 4-hour time limit. For more information on how to allocate resources on Tufts HPC cluster, check out:
    
    [Compute Resources :octicons-info-16:](../hpc-user-guide/compute-resources.md){:target="_blank" rel="noopener" .md-button .md-button--primary }

- Within the interactive session, you can start R 

```R
R
```

## Installing R packages

- In R, you can install the packages you need in your home directory with:

```R
install.packages("XXX")
```

- You can also use the packages installed in HPC Tools R package repo:

```R
LIB='/cluster/tufts/hpc/tools/R/4.0.0' 
.libPaths(c("",LIB))
```

- You can also use packages installed in BioTools R package repo:

```R
LIB='/cluster/tufts/bio/tools/R_libs/4.0.0' 
.libPaths(c("",LIB)) 
```

- If you are having trouble installing the packages you need, please contact [tts-research@tufts.edu](tts-research@tufts.edu).

     
- To exit from R command line interface:

```
q()
```
- To terminate interactive session 

```
exit
```

## R Package Installation Troubleshooting

**Suggestion 1: Try installing the R package from command line instead of RStudio OnDemand**

- The RStudio OnDemand interface is not perfect and can store things like different libPaths between sessions. To be safe, it is always best to install new R package from the command line when on the Tufts HPC.
    
**Suggestion 2: You may need to load more modules**

- On the Tufts HPC you load modules of software that might already be installed on your machine. This is why it can be easier to install R packages on your local machine rather than the Tufts HPC. If you are unsuccessful at installing an R package, try loading the following modules:
    
```
module load curl/7.47.1 gcc/7.3.0 hdf5/1.10.4 boost/1.63.0-python3 libpng/1.6.37 java/1.8.0_60 libxml2/2.9.10 libiconv/1.16 fftw/3.3.2 gsl/2.6 R/4.0.0
```

**Suggestion 3: Take a look at the last few lines of the error message**

- The error message will give you a clue as to what is going wrong. For example a common example:
    
```
Error in loadNamespace(j <- i[[1L]], c(lib.loc, .libPaths()), versionCheck = vI[[j]]) : 
  {==there is no package called ???Rcpp???==}
Error: package or namespace load failed for ???ggplot2???
```

- Here you might need to install a dependency beforehand with either:
    
```
install.packages("Rcpp")
```

or:

```
install.packages("ggplot2",dependencies = TRUE)
```

**Suggestion 4: Install the package from the Repository**

- Dependant on the R module you are loading, you may be working with an older version of a package manager, like BiocManager. As such some of the packages might have dependencies that are deprecated. For example, when installing `APAlyzer`:
    
```
{==ERROR: dependency ???DESeq??? is not available for package ???APAlyzer???==}
* removing ???/cluster/home/user/R/x86_64-pc-linux-gnu-library/4.0/APAlyzer???

The downloaded source packages are in
	???/tmp/Rtmpraf0Ix/downloaded_packages???
Installation paths not writeable, unable to update packages
  path: /opt/shared/R/4.0.0/lib64/R/library
  packages:
    boot, class, cluster, codetools, foreign, KernSmooth, lattice, MASS,
    Matrix, mgcv, nlme, nnet, rpart, spatial, survival
Old packages: 'openssl', 'Seurat'
Update all/some/none? [a/s/n]: n
Warning message:
In install.packages(...) :
  installation of package ???APAlyzer??? had non-zero exit status
```

- We can try installing `APAlyzer` like so:
    
```
BiocManager::install('RJWANGbioinfo/APAlyzer')
```
