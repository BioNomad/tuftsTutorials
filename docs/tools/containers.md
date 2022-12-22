## Containers

Containers are a way of sharing software across different systems. On the Tufts HPC Cluster we can use the Singularity module (now called [Apptainer](https://apptainer.org/)) to build containers on the cluster. 

## Building A Container

- To begin you will need to load the following modules:

```
module load singularity/3.6.1
module load squashfs
```

- Now, search [docker hub](https://hub.docker.com/) for the tool of your choice. You will be using this image to build a singularity container or sif file. In this case we will be demonstrating biobakery:

```
singularity build bioBakery.sif docker://biobakery/workflows
```

## Using A Container

- To use this tool you will need to reference the sif file you created. So to run the humann2 command you would use the following:

```
singularity exec bioBakery.sif humann3 --help
```
