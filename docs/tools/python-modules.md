## Python Interactive Session

- Login to the HPC cluster either by Command Line or the OnDemand Website:

!!! info ""

    For information on how to log into the cluster check out:
    
    [Navigate To The Cluster :octicons-info-16: ](../hpc-user-guide/navigate-to-cluster.md){:target="_blank" rel="noopener" .md-button .md-button--primary }

- From the login node, load the python module 

```
module load python/3.8.8
```
     
!!! tip
    To check out different python modules enter the command `module av python` 

- Allocate computing resources. Start an interactive session with your desired number of cores and memory, here we are using 2 cores with 4GB of memory: 

```
srun -p interactive -n 2 --mem=4g --pty bash
```

!!! note
    Interactive partition has a default 4-hour time limit 

- For more information on how to allocate resources on Tufts HPC cluster, check out:

[Compute Resources :octicons-info-16:](../hpc-user-guide/compute-resources.md){:target="_blank" rel="noopener" .md-button .md-button--primary }


