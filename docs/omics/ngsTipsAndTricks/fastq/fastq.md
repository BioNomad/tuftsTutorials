## NGS Tips & Tricks

NGS data is widely used to assess RNA/DNA by providing insight into genome sequences, RNA transcription activity, and analyze epigenetic activity -  just to name a few applications. Manipulating this data can be difficult, so here we provide a few tips and tricks for manipulating Fastq data. 

### Counting Sequences in a Fastq File

- For a non-compressed Fastq file:

```bash
cat Mock_12hr_rep1.fastq | echo "$((`wc -l` / 4))"
```

- For a compressed Fastq file:

```bash
zcat Mock_12hr_rep1.fastq.gz | echo "$((`wc -l` / 4))"
```


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

### Quality Control

You can perform FastQC on your files and then MulitQC to aggregate these reports"

```bash
ls
```

!!! info "output"

    ```bash
    HIV_12hr_rep1.fastq.gz  HIV_12hr_rep2.fastq.gz  HIV_24hr_rep1.fastq.gz  HIV_24hr_rep2.fastq.gz  Mock_12hr_rep1.fastq.gz  Mock_12hr_rep2.fastq.gz
    ```
    
```bash
# make directory for output
mkdir fastqc

# load the fastqc module
module load fastqc

# run fastqc on all fastq files in this directory and output them to the fastqc directory
fastqc *fastq.gz -o fastqc
```

!!! example "Explanation of Arguments"

    - `fastqc` run fastqc
    - `*fastq.gz` run fastqc on all fastq files in this directory
    - `-o fastqc`  output the results to the fastqc directory
    
- To collate these reports into one report:

```bash
ls
```

!!! info "output"

    ```bash
    fastqc  HIV_12hr_rep1.fastq.gz  HIV_12hr_rep2.fastq.gz  HIV_24hr_rep1.fastq.gz  HIV_24hr_rep2.fastq.gz  Mock_12hr_rep1.fastq.gz  Mock_12hr_rep2.fastq.gz
    ```
    
```bash
# make multiqc directory
mkdir multiqc

# run multiqc on fastqc results
multiqc fastqc/ -o multiqc/
```

!!! example "Explanation of Arguments"

    - `multiqc` run multiqc
    - `fastqc/ ` input directory with fastqc results
    - `-o multiqc/`  output the results to the multiqc directory
