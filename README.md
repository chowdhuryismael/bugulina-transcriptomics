# bugulina-transcriptomics

## Tierburg Bugulina stolonifera

## SRA collection
    #!/usr/bin/env bash
    
    # Create directories
    mkdir -p fastq sra
    
    # === STEP 1: Download SRA files ===
    echo "Downloading SRA files..."
    
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096640/SRR11096640.sra -o sra/autozooid_bud_rep1.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096639/SRR11096639.sra -o sra/autozooid_bud_rep2.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096638/SRR11096638.sra -o sra/avicularium_mature_rep1.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096637/SRR11096637.sra -o sra/avicularium_mature_rep2.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096636/SRR11096636.sra -o sra/rhizoid_autozooid_rep1.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096635/SRR11096635.sra -o sra/rhizoid_autozooid_rep2.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096634/SRR11096634.sra -o sra/rhizoid_autozooid_rep3.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096633/SRR11096633.sra -o sra/rhizoid_network_rep1.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096632/SRR11096632.sra -o sra/rhizoid_network_rep2.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096631/SRR11096631.sra -o sra/rhizoid_network_rep3.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096629/SRR11096629.sra -o sra/autozooid_bud_rep3.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096628/SRR11096628.sra -o sra/autozooid_mature_rep1.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096627/SRR11096627.sra -o sra/autozooid_mature_rep2.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096626/SRR11096626.sra -o sra/autozooid_mature_rep3.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096625/SRR11096625.sra -o sra/avicularium_bud_rep1.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096624/SRR11096624.sra -o sra/avicularium_bud_rep2.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096623/SRR11096623.sra -o sra/avicularium_bud_rep3.sra
    curl -L ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR110/SRR11096622/SRR11096622.sra -o sra/avicularium_mature_rep3.sra
    
    echo "Download complete!"
    
    # === STEP 2: Extract FASTQ files ===
    echo "Extracting FASTQ files..."
    module load sra-toolkit
    
    for sra_file in sra/*.sra; do
        name=$(basename "$sra_file" .sra)
        echo "Extracting $name..."
        fasterq-dump "$sra_file" --split-files --outdir fastq/
    done
    
    # === STEP 3: Compress ===
    echo "Compressing FASTQ files..."
    gzip fastq/*.fastq
    
    echo "All done!"


    #!/usr/bin/env bash
    # Run this from /p/h/b/b/k/i/t/R/tierberg_reads
    
    # Create tissue directories
    mkdir -p autozooid_bud
    mkdir -p autozooid_mature
    mkdir -p avicularium_bud
    mkdir -p avicularium_mature
    mkdir -p rhizoid_autozooid
    mkdir -p rhizoid_network
    
    # Move files to their respective directories
    mv autozooid_bud_rep*.fastq.gz autozooid_bud/
    mv autozooid_mature_rep*.fastq.gz autozooid_mature/
    mv avicularium_bud_rep*.fastq.gz avicularium_bud/
    mv avicularium_mature_rep*.fastq.gz avicularium_mature/
    mv rhizoid_autozooid_rep*.fastq.gz rhizoid_autozooid/
    mv rhizoid_network_rep*.fastq.gz rhizoid_network/
    
    # Verify
    echo "=== Files per directory ==="
    for dir in autozooid_bud autozooid_mature avicularium_bud avicularium_mature rhizoid_autozooid rhizoid_network; do
        count=$(ls $dir/*.fastq.gz 2>/dev/null | wc -l)
        echo "$dir: $count files"
    done

## FastQC

    for tissue in autozooid_bud autozooid_mature avicularium_bud avicularium_mature rhizoid_autozooid rhizoid_network; echo "Running FastQC on $tissue..."; fastqc $tissue/*.fastq.gz -o fastqc_reports/; end
    # Create directory for multiqc output
    
    mkdir -p multiqc_report
    
    # Run multiqc
    multiqc fastqc_reports/ -o multiqc_report/

## Trimmed
  mkdir -p trimmed

    for tissue in autozooid_bud autozooid_mature avicularium_bud avicularium_mature rhizoid_autozooid rhizoid_network
        for rep in rep1 rep2 rep3
            set r1 $tissue/$tissue\_$rep\_R1.fastq.gz
            set r2 $tissue/$tissue\_$rep\_R2.fastq.gz
            set out1 trimmed/$tissue\_$rep\_R1.fastq.gz
            set out2 trimmed/$tissue\_$rep\_R2.fastq.gz
            set html trimmed/$tissue\_$rep\_fastp.html
            set json trimmed/$tissue\_$rep\_fastp.json
            
            echo "Trimming $tissue $rep..."
            fastp -i $r1 -I $r2 -o $out1 -O $out2 --detect_adapter_for_pe -q 20 -l 50 -w 4 -h $html -j $json
        end
    end

## Salmon
    # Create a directory for the index
    mkdir -p salmon_index
    
    # Build the index
    salmon index \
        -t Trinity_2019filtered_Reference.fasta \
        -i salmon_index/Bstol_index \
        -p 8
