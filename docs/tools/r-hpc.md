# R on the HPC

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

## R batch jobs

- 1. Login to the HPC cluster 

  2. Upload your R script to the HPC cluster

  3. Go to the directory/folder which contains your R script

  4. Open your favorite text editor and write a slurm submission script similar to the following one `batchjob.sh` (name your own)

     ```
     #!/bin/bash
     #SBATCH -J myRjob  #job name
     #SBATCH --time=00-00:20:00 #requested time
     #SBATCH -p batch  #running on "batch" partition/queue
     #SBATCH -n 2  #2 cores total
     #SBATCH --mem=2g #requesting 2GB of RAM total
     #SBATCH --output=myRjob.%j.out #saving standard output to file
     #SBATCH --error=myRjob.%j.err  #saving standard error to file
     #SBATCH --mail-type=ALL  #email optitions
     #SBATCH --mail-user=Your_Tufts_Email @tufts.edu
     module load R/4.0.0
     Rscript --no-save your_rscript_name.R
     ```
5. Submit it with 
  
   `$ sbatch batchjob.sh`
   
6. If you are submitting multiple batch jobs to run the same script on different datasets, please make sure they are saving results to different files inside of your R script.

   

## RStudio Interactive App on OnDemand

1. Go to [OnDemand](https://ondemand.cluster.tufts.edu) Login with your username and password
2. Go to `Interactive Apps` tab and select `RStudio`
3. Select the time, number of cores, CPU memory you need, as well as the version of R you wish to run. 

![](images/r-studio-pax.png)

4. Load the module you need for your packages to run, if no additional modules are needed, leave it blank.
5. Each user can only start one OnDemand RStudio session on one compute node at a time. If you need to start multiple RStudio sessions, please make sure you select a different nodename from your current running session. 
6. Click "Launch" and wait for available resources
7. Once it's ready, click on the `Connect to RStudio` button
8. When you finished, exit RStudio properly `q()`, then close the RStudio tab, and go back to the main page click `Delete` to end the session

