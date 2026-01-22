# Sense check that fastq header edit hasn't changed or removed the number of sequences

## Check line count for original fastq 

Line count script: fastq_pre_edit_stats.sh 

        #!/bin/bash -l

        ############# SLURM SETTINGS #############
        #SBATCH --account=project0005
        #SBATCH --job-name=fastq_stats
        #SBATCH --output=%x-%J.out
        #SBATCH --error=%x-%J.err
        #SBATCH --time=0-40:00:00
        #SBATCH --mem=12G
        #SBATCH --ntasks=1
        #SBATCH --cpus-per-task=12
        #SBATCH --ntasks-per-node=1
        #SBATCH --mail-user=paul.b.campbell@glasgow.ac.uk
        #SBATCH --mail-type=ALL

        ############# LOADING MODULES #############
        module load pigz

        ############# MY CODE #############

        OUTFILE="fastq_header_pre_edit_stats.txt"

        # Clear output file
        : > "${OUTFILE}"

        # Header printing function
        print_header () {
            {
        echo "========================================"
        echo "$1"
        echo "========================================"
            } >> "${OUTFILE}"
        }

        # List of files
        FILES=(
            farm_1_posttx_R1_001.fastq.gz
            farm_1_posttx_R2_001.fastq.gz
            farm_1_pretx_R1_001.fastq.gz
            farm_1_pretx_R2_001.fastq.gz
            farm_2_posttx_R1_001.fastq.gz
            farm_2_posttx_R2_001.fastq.gz
            farm_2_pretx_R1_001.fastq.gz
            farm_2_pretx_R2_001.fastq.gz
            farm_3_posttx_R1_001.fastq.gz
            farm_3_posttx_R2_001.fastq.gz
            farm_3_pretx_R1_001.fastq.gz
            farm_3_pretx_R2_001.fastq.gz
        )

        ########### LINE COUNTS ###########
        print_header "Line counts (total number of lines)"

        for f in "${FILES[@]}"; do
            echo "${f}:" >> "${OUTFILE}"
            pigz -dc -p 12  "$f" | wc -l >> "${OUTFILE}"
            echo >> "${OUTFILE}"
        done


Output:  fastq_header_pre_edit_stats.txt 

        ========================================
        Line counts (total number of lines)
        ========================================
        farm_1_posttx_R1_001.fastq.gz:
        4852304172

        farm_1_posttx_R2_001.fastq.gz:
        4852304172

        farm_1_pretx_R1_001.fastq.gz:
        5732524524

        farm_1_pretx_R2_001.fastq.gz:
        5732524524

        farm_2_posttx_R1_001.fastq.gz:
        4319586440

        farm_2_posttx_R2_001.fastq.gz:
        4319586440

        farm_2_pretx_R1_001.fastq.gz:
        5044210024

        farm_2_pretx_R2_001.fastq.gz:
        5044210024

        farm_3_posttx_R1_001.fastq.gz:
        4980432984

        farm_3_posttx_R2_001.fastq.gz:
        4980432984

        farm_3_pretx_R1_001.fastq.gz:
        4418444788

        farm_3_pretx_R2_001.fastq.gz:
        4418444788

## Check line count for edited fastq 

Line count script: fastq_post_edit_stats.sh 

        #!/bin/bash -l

        ############# SLURM SETTINGS #############
        #SBATCH --account=project0005
        #SBATCH --job-name=fastq_stats
        #SBATCH --output=%x-%J.out
        #SBATCH --error=%x-%J.err
        #SBATCH --time=0-40:00:00
        #SBATCH --mem=12G
        #SBATCH --ntasks=1
        #SBATCH --cpus-per-task=12
        #SBATCH --ntasks-per-node=1
        #SBATCH --mail-user=paul.b.campbell@glasgow.ac.uk
        #SBATCH --mail-type=ALL

        ############# LOADING MODULES #############

        module load pigz

        ############# MY CODE #############

        OUTFILE="fastq_header_post_edit_stats.txt"

        # Clear output file
        : > "${OUTFILE}"

        # Header printing function
        print_header () {
            {
                echo "========================================"
                echo "$1"
                echo "========================================"
            } >> "${OUTFILE}"
        }

        # List of files
        FILES=(
            farm_1_posttx_R1_001.fastq_renamed.fastq.gz
            farm_1_posttx_R2_001.fastq_renamed.fastq.gz
            farm_1_pretx_R1_001.fastq_renamed.fastq.gz
            farm_1_pretx_R2_001.fastq_renamed.fastq.gz
            farm_2_posttx_R1_001.fastq_renamed.fastq.gz
            farm_2_posttx_R2_001.fastq_renamed.fastq.gz
            farm_2_pretx_R1_001.fastq_renamed.fastq.gz
            farm_2_pretx_R2_001.fastq_renamed.fastq.gz
            farm_3_posttx_R1_001.fastq_renamed.fastq.gz
            farm_3_posttx_R2_001.fastq_renamed.fastq.gz
            farm_3_pretx_R1_001.fastq_renamed.fastq.gz
            farm_3_pretx_R2_001.fastq_renamed.fastq.gz
        )

        ########### LINE COUNTS ###########
        print_header "Line counts (total number of lines)"

        for f in "${FILES[@]}"; do
            echo "${f}:" >> "${OUTFILE}"
            pigz -dc -p 12  "$f" | wc -l >> "${OUTFILE}"
            echo >> "${OUTFILE}"
        done

Output: fastq_header_post_edit_stats.txt

        ========================================
        Line counts (total number of lines)
        ========================================
        farm_1_posttx_R1_001.fastq_renamed.fastq.gz:
        4852304172

        farm_1_posttx_R2_001.fastq_renamed.fastq.gz:
        4852304172

        farm_1_pretx_R1_001.fastq_renamed.fastq.gz:
        5732524524

        farm_1_pretx_R2_001.fastq_renamed.fastq.gz:
        5732524524

        farm_2_posttx_R1_001.fastq_renamed.fastq.gz:
        4319586440

        farm_2_posttx_R2_001.fastq_renamed.fastq.gz:
        4319586440

        farm_2_pretx_R1_001.fastq_renamed.fastq.gz:
        5044210024

        farm_2_pretx_R2_001.fastq_renamed.fastq.gz:
        5044210024

        farm_3_posttx_R1_001.fastq_renamed.fastq.gz:
        4980432984

        farm_3_posttx_R2_001.fastq_renamed.fastq.gz:
        4980432984

        farm_3_pretx_R1_001.fastq_renamed.fastq.gz:
        4418444788

        farm_3_pretx_R2_001.fastq_renamed.fastq.gz:
        4418444788





