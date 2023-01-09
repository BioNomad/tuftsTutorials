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


