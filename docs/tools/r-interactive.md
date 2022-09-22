## Running R on the HPC cluster

!!! note
    R version 3.5.0 is no longer usable on the new cluster Pax

## R Interactive Session

- 1. Login to the HPC cluster (new cluster Pax)

     `ssh your_username@login.pax.tufts.edu`

  2. From the login node, load R module 

     `$ module load R/4.0.0`

  3. If you need to install some packages, a lot of times, you may need a C compiler

     `$ module load gcc/7.3.0`

     Additional modules may need to be loaded, such as `sf/R_4.0.0` 

  4. Allocate computing resources. Start an interactive session with your desired number of cores and memory, here we are using 2 cores with 4GB of memory 

     `$ srun -p interactive -n 2 --mem=4g --pty bash`

     Note: Interactive partition has a default 4-hour time limit 

     For more information on how to allocate resources on Tufts HPC cluster, please reference: [Pax User Guide](https://tufts.box.com/v/Pax-User-Guide)

  5. Within the interactive session, you can start R 

     `$ R`

  6. 

     1. In R, you can install the packages you need in your home directory with:

        `> install.packages("XXX")`. 

     2.  You can also use the packages installed in HPC Tools R package repo:

        `> LIB='/cluster/tufts/hpc/tools/R/4.0.0' `

        `>.libPaths(c("",LIB)) `

     3. You can also use packages installed in BioTools R package repo:

        `> LIB='/cluster/tufts/bio/tools/R_libs/4.0.0' `

        `>.libPaths(c("",LIB)) `

     4.  If you are having trouble installing the packages you need, please contact tts-research@tufts.edu.

     

  7. Exit from R command line interface:

     `> q()`

  8. To terminate interactive session 

     `$ exit` 


