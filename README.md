# Read First

## Lab Group Directory

```bash
/mnt/vstor/SOM_PQHS_LXZ716
```


## Key Areas in CWRU HPC OnDemand Web Portal

The following figures provide a visual guide to key areas within the CWRU HPC OnDemand Web Portal that users frequently interact with.

- **Home Directory:**The location of the Home Directory in the CWRU HPC OnDemand Web Portal.
![](home_directory.jpg)

- **Active Jobs:** Where to view currently running jobs that have been submitted to SLURM.
![](active_job.jpg)

- **Pioneer Shell Access:** Where to access the Pioneer Shell to run your code on the HPC cluster.

![](shell_access.jpg)


## Bioinformatics Package Installation Status

This document lists various bioinformatics packages, their installation status, and links to their respective sections.


| Package  | Link to Section                          | Installed  |
|----------|------------------------------------------|------------|
| Woltka   | [Woltka](#woltka)                        | Yes        |
| Samtools | [Samtools](#samtools)                    | Yes        |
| Qiime 2  | [Qiime 2](#qiime-2)                      | Yes        |
| Kraken2  | [Kraken2](#kraken2)                      | Yes        |


# Submitting Batch Jobs

When running programs that take a very long time to complete, it's impractical to wait for them to run on your local machine or cluster interactively. Instead, you can submit these programs as batch jobs to a High-Performance Computing (HPC) cluster. This tutorial will guide you through creating and submitting a SLURM job script to run a batch job on an HPC cluster. We will be using the `sbatch` command to submit the job.

1. Create a SLURM Job Script:

A SLURM job script is a Bash script that contains directives for the SLURM workload manager. These directives specify resources such as the number of nodes, CPU cores, memory, job duration, and more. Below is a sample SLURM job script:


**YourFileName.slurm:**

```bash
#!/bin/bash
#SBATCH -N 3 # Requests 3 node for the job
#SBATCH -c 24 # Requests 24 CPU core
#SBATCH --mem-per-cpu=128G # Allocates 128 GB of memory per CPU core
#SBATCH --time=0-00:15:00 # 15 minutes
#SBATCH --output=my.stdout  # Directs the standard output to a file named "my.stdout"
#SBATCH --error=my.stderr # Directs the standard error to a file named "my.stderr"
#SBATCH --mail-user=abac123@case.edu # Specifies the email address to receive job notifications.
#SBATCH --mail-type=ALL # Sends email notifications for all events (job start, end, fail, etc.)
#SBATCH --job-name="just_a_test" # Names the job "just_a_test"

# Put commands for executing job below this line
# example:
module load Python 
python --version
```

2. Save the Job Script:
	
Save the script with a  `.slurm` extension. For example, save it as `YourFileName.slurm`.

3. Access the HPC Cluster:

Connect to the HPC cluster using `cluster/_pioneer Shell Access`.

4. Navigate to the Directory Containing Your SLURM Script:

Use the `cd` command to navigate to the directory where you saved `YourFileName.slurm`.

5. Submit the SLURM Job Script:
	
Use the sbatch command to submit your job script to the SLURM scheduler:

```bash
sbatch YourFileName.slurm
```

6. Monitor the Job:
You can check the progress of the job in the `Job/Active Jobs` section.

7. Check Job Output:

Once the job completes, check the output file (`my.stdout` in this example) for the results of your job. If the job failed, you can check the `my.stderr` file for the reason.

# Conda

Activate Conda:
Run the following command to activate Conda:

```bash
source /mnt/vstor/SOM_PQHS_LXZ716/software/miniconda3/bin/activate
```


# Woltka

[Woltka Github Link](https://github.com/qiyunzhu/woltka)


**Woltka** is a bioinformatics toolkit designed for microbiome studies that processes metagenomic sequencing data to produce taxonomic and functional profiles. It allows researchers to classify reads, aggregate them by various biological or functional units, and perform ecological and comparative analyses, making it useful for understanding microbial community structure and function.

<span style="color: red;">**Woltka is already installed in the Lab Group Conda environment.**</span>

Here is the way to access it:

1. Access the HPC Cluster:
Connect to the HPC cluster using `cluster/_pioneer Shell Access`.

2. Activate Conda:
Conda is already installed on the HPC. To activate Conda, run the following command:

```bash
source /mnt/vstor/SOM_PQHS_LXZ716/software/miniconda3/bin/activate
```

3. Activate the Woltka Environment:
To activate the Woltka environment, use the following command:

```bash
conda activate woltka
```

# Samtools

[Samtools Website](https://www.htslib.org/)

**Samtools** is a suite of programs used for interacting with high-throughput sequencing data, particularly in the context of microbiome research. It provides essential tools for manipulating and analyzing BAM, SAM, and CRAM files, which are formats for storing large nucleotide sequence alignments. In microbiome studies, Samtools is used to sort, index, and filter alignment data, enabling researchers to efficiently process and analyze metagenomic and metatranscriptomic sequences, assess microbial diversity, and identify microbial taxa and functional genes within complex microbial communities.


## Use Samtools

<span style="color: red;">Samtools already installed in group directory, you can just update your path to use samtools by running the following: <span>

```bash
export PATH=/mnt/vstor/SOM_PQHS_LXZ716/software/Samtools/bin:$PATH
```

To check if Samtools has been successfully installed, you can perform the following steps:

```bash
samtools --version
```

## Install Samtools
If you want to download and install your own Samtools, follow these steps:

1. Download the Source Code:

Download the source code for Samtools from the official website:

[https://www.htslib.org/download/](https://www.htslib.org/download/)

2. Upload to HPC:
Upload the downloaded file to your HPC environment.

3. Unzip the File:
Once uploaded, unzip the file using the following command:

```bash
tar -xvjf samtools-1.20.tar.bz2
```

4. Change Directory:
Navigate to the Samtools directory:

```bash
cd samtools-1.20
```

5. Configure the Installation:
Configure the installation by running (replace `/where/to/install` with your desired installation directory):

```bash
./configure --prefix=/where/to/install
```

6. Compile the Source Code:
Compile the source code using:
```bash
make
```

7. Install Samtools:
Install Samtools by running:

```bash
make install
```

8. Update Your PATH:
The executable programs will be installed in a `bin` subdirectory under your specified prefix. Add this directory to your `$PATH` to access the programs easily (replace `/where/to/install` with your specified installation directory):
```bash
export PATH=/where/to/install/bin:$PATH
```

#  QIIME 2

[QIIME 2 Website](https://qiime2.org/)

**Qiime 2** (Quantitative Insights Into Microbial Ecology 2) is a powerful, open-source bioinformatics platform designed for performing microbiome analysis from raw DNA sequencing data. It provides tools for the analysis and interpretation of high-throughput community sequencing data, facilitating tasks such as quality control, taxonomic classification, diversity analysis, and visualization. Qiime 2 supports a modular plugin system, enabling users to integrate various analytical methods and customize workflows, making it an essential tool for researchers studying microbial ecology, diversity, and function.

Qiime 2 is already installed in the Lab Group Conda environment. To use it, follow these steps:

1. Activate Conda:
Run the following command to activate Conda:

```bash
source /mnt/vstor/SOM_PQHS_LXZ716/software/miniconda3/bin/activate
```

2. Activate the Qiime 2 Environment:
Activate the Qiime 2 environment by running:

```bash
conda activate qiime2-amplicon-2024.5
```

3. Check the Version:
Run the following command to check if Qiime 2 is installed and to see the version number:
```bash
qiime --version
```

# Kraken2

[Kraken 2 Manual](https://github.com/DerrickWood/kraken2/wiki/Manual)

**Kraken2** is a highly efficient, open-source taxonomic classification system designed for metagenomic sequence data. It utilizes exact k-mer matches to classify sequences by comparing them to a database of known genomes, providing accurate and rapid identification of microbial taxa. Kraken2 is widely used in microbiome research for analyzing complex microbial communities, enabling researchers to classify millions of sequences in a matter of minutes. Its performance and accuracy make it a valuable tool for large-scale metagenomic studies, pathogen detection, and environmental microbiology.


Kraken2 is already installed. To copy Kraken2 binaries to your personal bin directory, run the following command:
```bash
cp /mnt/vstor/SOM_PQHS_LXZ716/software/Kraken2/kraken2{,-build,-inspect} $HOME/bin
```

Check the Version:
Run the following command to check if Kraken2 is installed and to see the version number:

```bash
kraken2 --version
```
