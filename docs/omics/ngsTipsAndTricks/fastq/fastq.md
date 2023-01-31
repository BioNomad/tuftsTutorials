## NGS Tips & Tricks

NGS data is widely used to assess RNA/DNA by providing insight into genome sequences, RNA transcription activity, and analyze epigenetic activity -  just to name a few applications. Manipulating this data can be difficult, so here we provide a few tips and tricks for manipulating Fastq data. 

### Counting Sequences in a Fastq File

- Counting sequences in a non-compressed fastq file:

```bash
cat Mock_12hr_rep1.fastq | echo "$((`wc -l` / 4))"
```

- Counting sequences in a compressed fastq file:

```bash
zcat Mock_12hr_rep1.fastq.gz | echo "$((`wc -l` / 4))"
```


### Subsampling a Fastq File

- Subsampling 10,000 sequences from paired fastq files using the same random seed (`-s100`) so that the same sequences are grabbed from each file:
- 
```bash
# load the anaconda module
module load anaconda/2021.11

# activate the conda environment
source activate /cluster/tufts/bio/tools/conda_envs/seqtk/1.3

# subsample the fastq file
seqtk sample -s100 fullData_R1.fastq.gz 10000 > subsampledData_R1.fastq.gz
seqtk sample -s100 fullData_R2.fastq.gz 10000 > subsampledData_R2.fastq.gz
```

### Quality Control

- Perform FastQC on your files and then MulitQC to aggregate these reports:
    
```bash
# make directory for output
mkdir fastqc

# load the fastqc module
module load fastqc

# run fastqc on all fastq files in this directory and output them to the fastqc directory
fastqc *fastq.gz -o fastqc
```

- To collate these reports into one report:
    
```bash
# make multiqc directory
mkdir multiqc

# run multiqc on fastqc results
multiqc fastqc/ -o multiqc/
```

### Convert Fastq to Fasta

```bash
# load the anaconda module
module load anaconda/2021.11

# activate the conda environment
source activate /cluster/tufts/bio/tools/conda_envs/seqtk/1.3

# convert fastq to fasta
seqtk seq -a someData.fastq.gz > someData.fasta
```
