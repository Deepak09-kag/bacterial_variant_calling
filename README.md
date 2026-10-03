# E. coli Whole Genome Sequencing Variant Calling

## Project Overview

This project demonstrates an end-to-end bacterial whole-genome sequencing (WGS) variant-calling workflow using *Escherichia coli* Illumina paired-end sequencing data.

## Objectives

- Process bacterial WGS sequencing data.
- Perform sequencing quality control.
- Remove low-quality bases and adapter sequences.
- Align reads to the *E. coli* K-12 MG1655 reference genome.
- Process and evaluate BAM alignment files.
- Identify genomic variants using BCFtools.
- Annotate variants using SnpEff.
- Validate the detected variant using alignment and pileup evidence.

## Dataset

- Sample: ERR008613
- Organism: *Escherichia coli*
- Sequencing: Illumina paired-end
- Data source: NCBI Sequence Read Archive (SRA)

## Reference Genome

- Accession: GCF_000005845.2
- Genome: *E. coli* K-12 MG1655
- Chromosome: NC_000913.3

## Workflow

SRA → FASTQ → FastQC → Trimmomatic → BWA → SAMtools → BCFtools → SnpEff → Variant Validation

## Detected Variant

- Position: NC_000913.3:4296380
- Reference: AC
- Alternate: ACGC
- Variant type: 2-bp insertion (GC)
- VCF depth: 238
- Effect: intergenic_region
- Impact: MODIFIER
- Region: gltP-yjcO intergenic region
- HGVS-like notation: n.4296381_4296382insGC

## Variant Validation

The variant was supported by primary alignment CIGAR evidence containing a 2-base insertion (2I) and by SAMtools mpileup insertion observations.

## Results

The detected 2-bp insertion is located in the intergenic region between gltP and yjcO. The analysis establishes the genomic location and annotation of the variant but does not establish a biological or phenotypic effect.

## Project Structure



## Skills Demonstrated

- Linux
- Bash
- Python
- NGS quality control
- FASTQ processing
- Read trimming
- BWA alignment
- SAM/BAM processing
- BCFtools variant calling
- SnpEff annotation
- Variant validation

## Conclusion

This project demonstrates a complete bacterial WGS variant-calling workflow from sequencing data through quality control, trimming, alignment, variant calling, annotation, and validation.
