## Python Interactive Session

1. Login to the HPC cluster (new cluster Pax)

     `ssh your_username@login.pax.tufts.edu`

2. From the login node, load the python module 

     `module load python/3.6.0`
     
!!! tip
    To check out different python modules enter the command `module av python` 

3. Allocate computing resources. Start an interactive session with your desired number of cores and memory, here we are using 2 cores with 4GB of memory 

     `srun -p interactive -n 2 --mem=4g --pty bash`

     Note: Interactive partition has a default 4-hour time limit 

     For more information on how to allocate resources on Tufts HPC cluster, please reference: [Pax User Guide](https://tufts.box.com/v/Pax-User-Guide)


