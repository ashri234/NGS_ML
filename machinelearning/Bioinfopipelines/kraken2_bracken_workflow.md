**Kraken2 and Bracken Classification Workflow**

This document outlines the steps I followed to process three metagenomic samples using Kraken2 and Bracken. The samples are:

- ERR14218891

- ERR14218664

- ERR14219004

Each sample was classified using Kraken2, and abundance estimation was refined with Bracken. I also extracted the classified and unclassified reads.

**Tools Required**

- Kraken2

- Bracken

**Workflow Overview**

For each sample, I performed the following steps:

Classify reads with Kraken2.
Extract classified and unclassified reads.
Estimate species abundance using Bracken.

🧬 **Sample: ERR14218891**

**Step 1: Kraken2 Classification**

```
kraken2 \
  --db /path/to/kraken2_db \
  --threads 16 \
  --report ERR14218891.k2report \
  --classified-out ERR14218891_classified.fastq \
  --unclassified-out ERR14218891_unclassified.fastq \
  --output ERR14218891.kraken2.out \
  ERR14218891.fastq
```

**Step 2: Bracken Species Estimation**

```
bracken \
  -d /path/to/kraken2_db \
  -i ERR14218891.k2report \
  -o ERR14218891_bracken_species.k2report \
  -r 150 \
  -l S
```

**🧬 Sample: ERR14218664**

**Step 1: Kraken2 Classification**
```
kraken2 \
  --db /path/to/kraken2_db \
  --threads 16 \
  --report ERR14218664.k2report \
  --classified-out ERR14218664_classified.fastq \
  --unclassified-out ERR14218664_unclassified.fastq \
  --output ERR14218664.kraken2.out \
  ERR14218664.fastq
```


**Step 2: Bracken Species Estimation**
```
bracken \
  -d /path/to/kraken2_db \
  -i ERR14218664.k2report \
  -o ERR14218664_bracken_species.k2report \
  -r 150 \
  -l S
```

**🧬 Sample: ERR14219004**
**Step 1: Kraken2 Classification**
```
kraken2 \
  --db /path/to/kraken2_db \
  --threads 16 \
  --report ERR14219004.k2report \
  --classified-out ERR14219004_classified.fastq \
  --unclassified-out ERR14219004_unclassified.fastq \
  --output ERR14219004.kraken2.out \
  ERR14219004.fastq
```
**Step 2: Bracken Species Estimation**
```
bracken \
  -d /path/to/kraken2_db \
  -i ERR14219004.k2report \
  -o ERR14219004_bracken_species.k2report \
  -r 150 \
  -l S
```

**Output Files**
Each sample will produce the following output files:

- {sample}_classified.fastq
- {sample}_unclassified.fastq
- {sample}.kraken2.out
- {sample}.k2report
- {sample}_bracken_species.k2report

**Example Output (File Sizes You Might See)**
```
-rw-r--r--  ERR14218891_classified.fastq      ~1.4G
-rw-r--r--  ERR14218664_classified.fastq     ~11.2G
-rw-r--r--  ERR14219004_classified.fastq     ~10.6G
```
