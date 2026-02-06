# Alignment of *O.* *ostertagi* and *H.* *contortus* genome assembly 

This document describes the execution of **PROmer** (from the MUMmer package) to perform protein-level genome alignment between *Haemonchus contortus* and *Ostertagia ostertagi*, and visualise synteny using circos. PROmer aligns translated nucleotide sequences, improving sensitivity for divergent genomes.

### Command: Genome alignment using PROmer and maximal unique matches 
  
    promer \
    --prefix=oster_vs_hcon \
    --mum \
    /users/pbc1s/project0005/paul/ref_genomes/soft-masked_genome/haemonchus_contortus.PRJEB506.WBPS19.genomic_softmasked.fa \
    /users/pbc1s/project0005/paul/ref_genomes/unmasked_genome/GCA_964213955.1_nxOstOste4.1_genomic.fna


### Parameter description: 

| **Parameter** | **Function**  |
|---------------|---------------|
|promer | Specify alignment package	|
|--prefix | Defines naming prefix |
|--mum | Use maximal unique matches |


### Output files:
	•	oster_vs_hcon.delta – Alignment coordinates
	•	oster_vs_hcon.mums 	– Match coordinates

## Processing PROmer alignment using **show-ccords** from the MUMmer package. 

The goal is to generate a filtered and human-readable alignment coordinate file for downstream comparative genomics analyses.

### Command: Generate alignment coordinates

	show-coords \
  		-lTH \
  		-L 500 \
  		oster_vs_hcon.delta > oster_vs_hcon.coords

### Parameter description: 

| **Parameter** | **Function**  |
|---------------|---------------|
| -l 			|Include alignment length|
|-T				|Produce tab-delimited output|
|-H				|Suppress header lines |
-L 1000			|Filter alignments shorter than 500 aa|

### Output files:
	•	oster_vs_hcon.coords

## Circos Input Generation from PROMmer Coordinates

This step converts filtered MUMmer alignment coordinates into Circos-compatible configuration and link files. The script processes genome alignment data to generate ribbon-style synteny visualisations.

### Command: Run NUCmer.2.circos.pl 

	/usr/bin/perl \
	//users/pbc1s/project0005/paul/chr_synteny/promer_synteny/nucmer.2.circos.pl \
   		--promer \
    	--min_hit_len=1000 \
    	--min_chr_len=20000 \
    	--ribbons \
    	--prefix oster_vs_hcon \
    	--debug \
   		--coord-file oster_vs_hcon.coords \
    	--flipquery \
    	--colour_links_by_query

### Parameter description: 

| **Parameter** | **Function**  |
|---------------|---------------|
|--promer |Specifies that input coordinates originate from PROmer |
|--min_chr_len=20000 | Excludes scaffolds shorter than 20kb |
|--ribbons | Produce ribbon-style synteny links |
|--prefix | Defines naming prefix |
|--debug | Produces verbose output for troubleshooting |
|--coord-file | Specifies filtered input file |
|--flipquery | Reverses orientation of query genome relative to reference |
|--colour_links_by_query | Colours ribbons based on query chromosome identity |

### Output files:

	•	karyotype file
	•	link data file 
	•	circos configuration file 

## Generate circos plot 

This step generates a Circos visualisation using pre-prepared configuration and data files. The Circos software produces circular genome plots used to visualise structural relationships such as synteny and chromosomal rearrangements.

### Command: Run circos 

	circos -conf circos.conf

### Output files:

	•	PNG image of synteny plot
	•	SVG file
	•	Log files for troubleshooting

![Genome synteny between *O. ostertagi* and *H. contortus*.](figures/oster_vs_hconcircos.png)




