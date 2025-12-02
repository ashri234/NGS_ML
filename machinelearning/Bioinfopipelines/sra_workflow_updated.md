
**SRA Data Download and Processing Workflow**

This document describes my workflow for downloading and processing Sequence Read Archive (SRA) data using the NCBI SRA Toolkit for a training course. I will execute specific Linux commands to set up the environment, download SRA files for three samples from BioProject PRJEB72526, and convert them to FASTQ format.

**Purpose**

For this training course, I will download SRA data from the NCBI database for three samples (ERR14218891, ERR14218664, and ERR14219004) from BioProject PRJEB72526 and generate FASTQ files for genomic analysis, such as RNA-Seq or metagenomics. I will use the prefetch and fastq-dump commands in a Linux environment.

**Prerequisites**

Before starting, I will ensure the following are set up:

- Conda Installation: Miniconda or Anaconda must be installed on the Linux system. If not, follow the Miniconda installation guide.
- Input Parameters:
Output directory: sra_data
SRA IDs: ERR14218891, ERR14218664, ERR14219004
FASTQ directories: sra_data/<SRA_ID>
SRA file paths: sra_data/<SRA_ID>/<SRA_ID>.sra
- System Requirements: Linux system with bash, sufficient storage, and write permissions.
**Step-by-Step Workflow**
I will follow these steps to set up the environment, download, and process SRA data. Each step includes the exact Linux command I will execute, its purpose, and what I expect to happen.

**Step 1: Create and Activate Conda Environment**
```
conda create -n sra python=3.8
conda activate sra
```
**Step 2: Install SRA Toolkit**
I will install the SRA Toolkit using the bioconda channel
```
conda install -c bioconda sra-tools
```
**Step 3: Create Output Directory**
Then create a folder to store the output name sra_data

mkdir -p sra_data
**Step 4: Download SRA Files**
```
prefetch --output-directory sra_data ERR14218891
prefetch --output-directory sra_data ERR14218664
prefetch --output-directory sra_data ERR14219004
```
**Step 5: Create FASTQ Directories**
```
mkdir -p sra_data/ERR14218891
mkdir -p sra_data/ERR14218664
mkdir -p sra_data/ERR14219004
```
**Step 6: Convert to FASTQ**

I am going to use the following command to convert .sra files into compressed FASTQ files using fastq-dump:

This step ensures that we generate high-quality, compressed FASTQ files from the .sra archive, suitable for downstream analysis.
```
fastq-dump --outdir sra_data/ERR14218891 --gzip --skip-technical --readids --read-filter pass --dumpbase --split-files --clip sra_data/ERR14218891/ERR14218891.sra

fastq-dump --outdir sra_data/ERR14218664 --gzip --skip-technical --readids --read-filter pass --dumpbase --split-files --clip sra_data/ERR14218664/ERR14218664.sra

fastq-dump --outdir sra_data/ERR14219004 --gzip --skip-technical --readids --read-filter pass --dumpbase --split-files --clip sra_data/ERR14219004/ERR14219004.sra
```
**Purpose**: Convert the SRA file to FASTQ format, with options to:

- Output to sra_data/ERR14218891.
- Compress output files with gzip (--gzip).
- Skip technical reads (--skip-technical).
- Include read IDs (--readids).
- Filter passing reads (--read-filter pass).
- Use base calls (--dumpbase).
- Split paired-end reads into separate files (--split-files).
- Clip adapters (--clip).
**Step 7: Verify Outputs**
```
ls -lh sra_data/ERR14218891/
ls -lh sra_data/ERR14218664/
ls -lh sra_data/ERR14219004/
```
Purpose: ls -lh List the contents of the FASTQ directory to verify the presence and size of FASTQ files, logging the output.

**Complete Command Sequence**
```
conda create -n sra python=3.8
conda activate sra
conda install -c bioconda sra-tools
mkdir -p sra_data
prefetch --output-directory sra_data ERR14218891
prefetch --output-directory sra_data ERR14218664
prefetch --output-directory sra_data ERR14219004
mkdir -p sra_data/ERR14218891
mkdir -p sra_data/ERR14218664
mkdir -p sra_data/ERR14219004
fastq-dump --outdir sra_data/ERR14218891 --gzip --skip-technical --readids --read-filter pass --dumpbase --split-files --clip sra_data/ERR14218891/ERR14218891.sra
fastq-dump --outdir sra_data/ERR14218664 --gzip --skip-technical --readids --read-filter pass --dumpbase --split-files --clip sra_data/ERR14218664/ERR14218664.sra
fastq-dump --outdir sra_data/ERR14219004 --gzip --skip-technical --readids --read-filter pass --dumpbase --split-files --clip sra_data/ERR14219004/ERR14219004.sra
ls -lh sra_data/ERR14218891/
ls -lh sra_data/ERR14218664/
ls -lh sra_data/ERR14219004/
```
**Example of Output Files**
Once the downloading and FASTQ conversion steps are successfully completed, your output directory will contain files similar to the ones listed below:
```
-rw-r--r-- 1 user group 1864543084 Aug  1 20:39 ERR14218891_pass_1.fastq.gz  
-rw-r--r-- 1 user group 1920189678 Aug  1 20:39 ERR14218891_pass_2.fastq.gz  
-rw-r--r-- 1 user group 2427275592 Aug  1 20:39 ERR14218891.sra  
-rw-r--r-- 1 user group 1844548218 Aug  1 20:40 ERR14218664_pass_1.fastq.gz  
-rw-r--r-- 1 user group 1891657137 Aug  1 20:41 ERR14218664_pass_2.fastq.gz  
-rw-r--r-- 1 user group 2387906889 Aug  1 20:41 ERR14218664.sra  
-rw-r--r-- 1 user group 1617531248 Aug  1 20:41 ERR14219004_pass_1.fastq.gz  
-rw-r--r-- 1 user group 1627314348 Aug  1 20:42 ERR14219004_pass_2.fastq.gz  
-rw-r--r-- 1 user group 2060741013 Aug  1 20:42 ERR14219004.sra
```
End of the workflow.

**References**

- [NCBI SRA Toolkit Documentation](https://www.ncbi.nlm.nih.gov/sra/docs/sra-dowload-tools/)

- [NCBI SRA Database](https://www.ncbi.nlm.nih.gov/sra)

- [NCBI SRA Download Guide](https://www.ncbi.nlm.nih.gov/sra/docs/sradownload/)
