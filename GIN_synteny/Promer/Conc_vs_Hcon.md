# Alignment of *O.* *ostertagi* and *H.* *contortus* genome assembly 

This document describes the execution of **PROmer** (from the MUMmer package) to perform protein-level genome alignment between *Haemonchus contortus* and *Ostertagia ostertagi*, and visualise synteny using circos. PROmer aligns translated nucleotide sequences, improving sensitivity for divergent genomes.

## Genome alignment using PROmer and maximal unique matches 
### Command
  
    promer \
    --prefix=oster_vs_hcon \
    --mum \
    /users/pbc1s/project0005/paul/ref_genomes/soft-masked_genome/haemonchus_contortus.PRJEB506.WBPS19.genomic_softmasked.fa \
    /users/pbc1s/project0005/paul/ref_genomes/unmasked_genome/GCA_964213955.1_nxOstOste4.1_genomic.fna

### Output files:
	•	oster_vs_hcon.delta – Alignment coordinates
	•	oster_vs_hcon.mums 	– Match coordinates

## Processing PROmer alignment using **show-ccords** from the MUMmer package. 

The goal is to generate a filtered and human-readable alignment coordinate file for downstream comparative genomics analyses.

## Generate alignment coordinates
### Command

	show-coords \
  		-lTH \
  		-L 1000 \
  		oster_vs_hcon.delta > oster_vs_hcon.coords

### Parameter description 

| **Parameter** | **Function**  |
|---------------|---------------|
| -l 			|Include alignment length|
|-T				|Produce tab-delimited output|







