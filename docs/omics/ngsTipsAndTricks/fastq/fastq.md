## NGS Tips & Tricks

NGS data is widely used to assess RNA/DNA by providing insight into genome sequences, RNA transcription activity, and analyze epigenetic activity -  just to name a few applications. Manipulating this data can be difficult, so here we provide a few tips and tricks for manipulating Fastq data. 

### Subsampling a Fastq File

```bash
# load the anaconda module
module load anaconda/2021.11

# activate the conda environment
source activate /cluster/tufts/bio/tools/conda_envs/seqtk/1.3

# subsample the fastq file
seqtk sample -s100 fullData_R1.fastq.gz 10000 > subsampledData_R1.fastq.gz
seqtk sample -s100 fullData_R2.fastq.gz 10000 > subsampledData_R2.fastq.gz
```

!!! example "Explanation of Arguments"

    - `seqtk sample` subsample data
    - `-s100` random seed, so that the same lines are subsampled if working with paired data
    - `fullData_R1.fastq.gz`  full data, Forward reads
    - `fullData_R2.fastq.gz`  full data, Reverse reads
    - `10000` how many lines to subsample
    - `> subsampledData_R1.fastq.gz` assign to a new file
