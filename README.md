# 🧬 E. coli Whole-Genome Sequencing Variant Calling

> **End-to-end bacterial WGS variant-calling workflow using Illumina paired-end sequencing data**

This project demonstrates a complete **bioinformatics workflow for bacterial whole-genome sequencing (WGS)**, covering sequencing quality control, read preprocessing, reference alignment, BAM processing, variant calling, annotation, and validation.

---

## 🧬 Project Overview

The project analyzes Illumina paired-end sequencing data from *Escherichia coli* to identify genomic variation against the *E. coli* K-12 MG1655 reference genome.

The analysis follows a standard NGS variant-calling workflow:

```text
🧬 SRA
   ↓
🧪 FASTQ
   ↓
🔍 FastQC
   ↓
✂️ Trimmomatic
   ↓
🧬 BWA
   ↓
💻 SAMtools
   ↓
🧬 BCFtools
   ↓
🔬 SnpEff
   ↓
📊 Variant Validation
```

The project was performed in a **Linux/Ubuntu environment** using commonly used NGS and bioinformatics tools.

---

## 🎯 Objectives

The main objectives of this project were to:

* 🔍 Perform quality control of Illumina paired-end sequencing reads.
* ✂️ Remove low-quality bases and adapter sequences.
* 🧬 Align sequencing reads to the *E. coli* K-12 MG1655 reference genome.
* 💻 Process and evaluate BAM alignment files.
* 🧬 Identify genomic variants using BCFtools.
* 🔬 Annotate detected variants using SnpEff.
* ✅ Validate the detected variant using alignment and pileup evidence.
* 📊 Summarize the final variant and its genomic context.

---

## 🧪 Dataset

| Parameter              | Details                          |
| ---------------------- | -------------------------------- |
| 🧬 Sample              | `ERR008613`                      |
| 🦠 Organism            | *Escherichia coli*               |
| 🧪 Sequencing Platform | Illumina                         |
| 📚 Sequencing Type     | Paired-end                       |
| 🌐 Data Source         | NCBI Sequence Read Archive (SRA) |

---

## 🧬 Reference Genome

The sequencing reads were aligned against the *Escherichia coli* K-12 MG1655 reference genome.

| Parameter             | Details               |
| --------------------- | --------------------- |
| 🧬 Assembly Accession | `GCF_000005845.2`     |
| 🦠 Organism           | *E. coli* K-12 MG1655 |
| 🧬 Chromosome         | `NC_000913.3`         |

---

## 🔬 Analysis Workflow

```text
                    🧬 E. coli WGS Data
                            │
                            ▼
                    🌐 NCBI SRA Dataset
                            │
                            ▼
                     🧪 FASTQ Conversion
                            │
                            ▼
                         🔍 FastQC
                     Quality Assessment
                            │
                            ▼
                      ✂️ Trimmomatic
                   Adapter/Quality Trimming
                            │
                            ▼
                         🧬 BWA
                      Read Alignment
                            │
                            ▼
                       💻 SAMtools
                    BAM Processing & QC
                            │
                            ▼
                       🧬 BCFtools
                     Variant Calling
                            │
                            ▼
                        🔬 SnpEff
                    Variant Annotation
                            │
                            ▼
                      📊 Validation
                            │
                            ▼
                     ✅ Final Results
```

---

## 🛠️ Tools & Technologies

| Category                | Tools / Technologies |
| ----------------------- | -------------------- |
| 💻 Operating System     | Linux / Ubuntu       |
| 🌐 Data Source          | NCBI SRA             |
| 🔍 Quality Control      | FastQC               |
| ✂️ Read Trimming        | Trimmomatic          |
| 🧬 Read Alignment       | BWA                  |
| 💻 Alignment Processing | SAMtools             |
| 🧬 Variant Calling      | BCFtools             |
| 🔬 Variant Annotation   | SnpEff               |
| 🐍 Scripting            | Bash, Python         |
| 🌿 Version Control      | Git, GitHub          |

### 🔧 Tool Versions

| Tool        | Version           |
| ----------- | ----------------- |
| FastQC      | `0.12.1`          |
| Trimmomatic | `0.39`            |
| BWA         | `0.7.17-r1188`    |
| BCFtools    | `1.19`            |
| Java        | `OpenJDK 21.0.11` |

---

## 🔍 Quality Control & Read Preprocessing

Initial sequencing quality was evaluated using **FastQC**.

Reads were then processed using **Trimmomatic** with paired-end processing.

### ✂️ Trimming Parameters

```text
-threads 4
TruSeq3-PE.fa
LEADING:3
TRAILING:3
SLIDINGWINDOW:4:20
MINLEN:36
```

### 📊 Trimming Summary

| Metric                 |     Result |
| ---------------------- | ---------: |
| Input read pairs       | 14,214,324 |
| Both reads surviving   | 12,867,218 |
| Both surviving         |     90.52% |
| Forward-only surviving |    620,355 |
| Reverse-only surviving |    542,916 |
| Dropped reads          |    183,835 |
| Dropped                |      1.29% |

The trimming step removed low-quality sequence portions and adapter-associated sequence while retaining the majority of the paired-end reads.

---

## 🧬 Read Alignment

The processed reads were aligned against the *E. coli* K-12 MG1655 reference chromosome using **BWA**.

The resulting alignments were processed into BAM format using **SAMtools**.

Alignment quality was evaluated using:

```bash
samtools flagstat
```

### 📊 Alignment Summary

| Metric          |     Result |
| --------------- | ---------: |
| Total reads     | 25,736,360 |
| Mapped reads    |     99.99% |
| Properly paired |     99.90% |
| Duplicates      |          0 |

The alignment statistics indicate that the sequencing reads mapped successfully to the selected reference genome.

---

## 🧬 Variant Calling

Variants were identified from the processed BAM alignment using **BCFtools**.

The variant-calling workflow generated VCF files containing the detected genomic variation.

The primary variant identified in this analysis was subsequently investigated at the alignment and pileup levels.

---

## 🔬 Variant Annotation

Detected variants were annotated using **SnpEff** to determine their genomic context and predicted annotation category.

The identified variant was annotated as an **intergenic-region variant** located between the `gltP` and `yjcO` genomic regions.

> **Note:** Variant annotation describes the genomic context of a variant but does not by itself establish a biological or phenotypic effect.

---

## 🧬 Detected Variant

The primary detected variant is a **2-base insertion**.

| Field                 | Result                        |
| --------------------- | ----------------------------- |
| 🧪 Sample             | `ERR008613`                   |
| 🧬 Chromosome         | `NC_000913.3`                 |
| 📍 Position           | `4,296,380`                   |
| 🧬 Reference allele   | `AC`                          |
| 🧬 Alternate allele   | `ACGC`                        |
| 🔬 Variant type       | 2-bp insertion (`GC`)         |
| 📊 VCF depth          | `238`                         |
| 🔬 SnpEff effect      | `intergenic_region`           |
| 📌 Impact             | `MODIFIER`                    |
| 🧬 Genomic region     | `gltP-yjcO` intergenic region |
| 📝 HGVS-like notation | `n.4296381_4296382insGC`      |

---

## 🔬 Variant Validation

The detected insertion was further examined using alignment-level and pileup evidence.

The variant was supported by:

* 🧬 Primary alignment CIGAR evidence containing a **2-base insertion (`2I`)**.
* 💻 SAMtools `mpileup` insertion observations at the variant position.
* 🧬 The observed inserted sequence was consistent with the called **`GC` insertion**.

### ✅ Validation Summary

These independent checks support the presence of the detected insertion in the analyzed sequencing data.

---

## 📊 Results

### 🧬 Primary Finding

The analysis identified a:

```text
2-bp insertion (GC)
NC_000913.3:4296380
```

### 🔬 Annotation

The variant was annotated by SnpEff as:

```text
Effect  : intergenic_region
Impact  : MODIFIER
Region  : gltP-yjcO intergenic region
```

### ✅ Evidence

The variant was additionally supported by:

```text
Primary CIGAR evidence → 2I insertion
                +
SAMtools mpileup → insertion observations
```

The analysis establishes the genomic location and annotation of the detected variant. However, it does **not** establish whether the variant has a biological or phenotypic effect.

---

## 📁 Project Structure

```text
bacterial_variant_calling/
│
├── 📂 qc/
│   └── FastQC quality-control reports
│
├── 📂 results/
│   ├── variant_annotation.tsv
│   └── variant_summary.txt
│
├── 📂 variants/
│   ├── ERR008613_raw.vcf
│   ├── ERR008613_filtered.vcf
│   ├── ERR008613_haploid_raw.vcf
│   └── ERR008613_snpeff.vcf
│
├── 📂 scripts/
│   └── Analysis/helper scripts
│
├── 📂 docs/
│   └── Project documentation
│
├── 📂 raw_data/
│   └── Raw sequencing data
│
├── 📂 trimmed/
│   └── Trimmed FASTQ files
│
├── 📂 alignment/
│   └── BAM/SAM alignment files
│
├── 📂 reference/
│   └── Reference genome and index files
│
├── 📄 .gitignore
└── 📄 README.md
```

### 📦 Large Files

Large sequencing and intermediate analysis files are intentionally excluded from the Git repository using `.gitignore`.

These include:

* Raw SRA files
* FASTQ files
* BAM/SAM files
* Reference genome files
* Reference index files
* Other large intermediate files

This keeps the GitHub repository lightweight while preserving the important final results and documentation.

---

## 💡 Skills Demonstrated

### 🧬 Bioinformatics

* Whole-genome sequencing analysis
* NGS quality control
* FASTQ processing
* Read trimming
* Reference genome alignment
* SAM/BAM processing
* Variant calling
* Variant annotation
* Variant validation
* Genomic coordinate interpretation

### 🛠️ Bioinformatics Tools

* FastQC
* Trimmomatic
* BWA
* SAMtools
* BCFtools
* SnpEff

### 💻 Programming & Computing

* Linux / Ubuntu
* Bash / Shell scripting
* Python
* Git
* GitHub

---

## ⚠️ Limitations

* The analysis focuses on a single bacterial WGS sample.
* The detected variant is based on the available sequencing data and selected reference genome.
* Variant annotation describes genomic context but does not establish biological function.
* The detected intergenic variant would require additional experimental or biological evidence to determine its functional significance.
* Large raw sequencing and intermediate files are excluded from the GitHub repository.

---

## 🎓 Conclusion

This project demonstrates an end-to-end bacterial WGS variant-calling workflow, beginning with sequencing data retrieval and quality control and continuing through:

```text
🧪 Sequencing Data
       ↓
🔍 Quality Control
       ↓
✂️ Read Preprocessing
       ↓
🧬 Reference Alignment
       ↓
💻 BAM Processing
       ↓
🧬 Variant Calling
       ↓
🔬 Variant Annotation
       ↓
✅ Variant Validation
```

The workflow resulted in the identification and validation of a **2-bp insertion** in the *E. coli* K-12 MG1655 reference chromosome.

The project demonstrates practical experience with commonly used NGS tools and provides a portfolio example of bacterial genomics variant analysis.

---

## 👨‍💻 Author

### **Deepak Kag**

🎓 **M.Sc. Bioinformatics**

### Areas of Interest

* 🧬 Bioinformatics
* 🧬 Genomics
* 🧪 NGS Data Analysis
* 🔬 Variant Calling
* 💻 Computational Biology
* 📊 Bioinformatics Data Analysis

---

## ⭐ Project Highlights

```text
🧬 Bacterial WGS
🔍 NGS Quality Control
✂️ Read Trimming
🧬 BWA Alignment
💻 SAM/BAM Processing
🧬 BCFtools Variant Calling
🔬 SnpEff Annotation
✅ Variant Validation
🐍 Python & Bash
🌿 Git & GitHub
```
