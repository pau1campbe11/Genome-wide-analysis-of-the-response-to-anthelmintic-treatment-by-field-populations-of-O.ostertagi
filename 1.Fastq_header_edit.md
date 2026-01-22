# Fastq header edit 
The fastq header format isn't recognised by bwa-mem tool currently on SLURM. Therefore, the header needs to be reformatted. 

Reformatting script: fastq_header_edit.sh 

    #!/bin/bash -l

    ############# SLURM SETTINGS #############
    #SBATCH --account=project0005
    #SBATCH --job-name=fastq_edit
    #SBATCH --output=%x-%J.out
    #SBATCH --error=%x-%J.err
    #SBATCH --time=0-30:00:00
    #SBATCH --mem=10G
    #SBATCH --ntasks=1
    #SBATCH --cpus-per-task=10
    #SBATCH --ntasks-per-node=1
    #SBATCH --mail-user=paul.b.campbell@glasgow.ac.uk
    #SBATCH --mail-type=ALL

    ############# LOADING MODULES #############

    ############# USER-DEFINED PATHS #########
    INPUT_DIR="/users/pbc1s/project0005/paul/0.original_fastq"
    OUTPUT_DIR="/users/pbc1s/project0005/paul/1.header_edit"

    mkdir -p "$OUTPUT_DIR"

    ############# MY CODE #####################

    for i in "$INPUT_DIR"/farm_*R[1-2]_001.fastq.gz; do
      base=$(basename "$i")
      zcat "$i" |
      awk 'NR % 4 == 1 { gsub(/1:N:0|2:N:0/, "BC:Z") } { print }' |
      pigz -p 10 > "$OUTPUT_DIR/${base%.gz}_renamed.fastq.gz"
    done
