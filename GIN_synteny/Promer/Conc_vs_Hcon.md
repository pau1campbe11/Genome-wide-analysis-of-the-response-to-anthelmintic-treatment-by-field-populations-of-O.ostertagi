# Alignment of *O.* *ostertagi* and *H.* *contortus* genome assembly 

This document describes the execution of **PROmer** (from the MUMmer package) to perform protein-level genome alignment between *Haemonchus contortus* and *Ostertagia ostertagi*. PROmer aligns translated nucleotide sequences, improving sensitivity for divergent genomes.

## Genome alignment using PROmer and maximal unique matches 
  
    promer \
    --prefix=oster_vs_hcon \
    --mum \
    /users/pbc1s/project0005/paul/ref_genomes/soft-masked_genome/haemonchus_contortus.PRJEB506.WBPS19.genomic_softmasked.fa \
    /users/pbc1s/project0005/paul/ref_genomes/unmasked_genome/GCA_964213955.1_nxOstOste4.1_genomic.fna

### Output files:
	•	oster_vs_hcon.delta – Alignment coordinates
	•	oster_vs_hcon.coords – Processed alignment summary (after delta filtering)
	•	oster_vs_hcon.mums – Match coordinates
