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
