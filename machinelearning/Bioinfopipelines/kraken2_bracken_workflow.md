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

Step 1: Kraken2 Classification

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
