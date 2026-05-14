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
## Quantifying tissue reads


    mkdir -p quants
    
    for tissue in autozooid_bud autozooid_mature avicularium_bud avicularium_mature rhizoid_autozooid rhizoid_network
        switch $tissue
            case autozooid_bud; set short AutoBud
            case autozooid_mature; set short AutoMat
            case avicularium_bud; set short AvicBud
            case avicularium_mature; set short AvicMat
            case rhizoid_autozooid; set short RhizAuto
            case rhizoid_network; set short RhizStol
        end
        
        for rep in rep1 rep2 rep3
            set r1 trimmed/$tissue\_$rep\_R1.fastq.gz
            set r2 trimmed/$tissue\_$rep\_R2.fastq.gz
            
            echo "Quantifying $short $rep..."
            salmon quant \
                -i salmon_index/Bstol_index \
                -l A \
                -1 $r1 \
                -2 $r2 \
                --validateMappings \
                -p 8 \
                -o quants/$short\_$rep
        end
    end








____________________________________________________________________________________________________
####################################################################################################
____________________________________________________________________________________________________
 ## Rstudio code

    setwd("C:/Users/chois652/OneDrive - University of Otago/Desktop/PhD thesis/thesis paper/genetic/Bryozoa RNA/bugulina stolonifera")
    getwd()
    library(tximport)
    library(DESeq2)

# List quant files
    files <- c(
      "quants/AutoBud_rep1/quant.sf", "quants/AutoBud_rep2/quant.sf", "quants/AutoBud_rep3/quant.sf",
      "quants/AutoMat_rep1/quant.sf", "quants/AutoMat_rep2/quant.sf", "quants/AutoMat_rep3/quant.sf",
      "quants/AvicBud_rep1/quant.sf", "quants/AvicBud_rep2/quant.sf", "quants/AvicBud_rep3/quant.sf",
      "quants/AvicMat_rep1/quant.sf", "quants/AvicMat_rep2/quant.sf", "quants/AvicMat_rep3/quant.sf",
      "quants/RhizAuto_rep1/quant.sf", "quants/RhizAuto_rep2/quant.sf", "quants/RhizAuto_rep3/quant.sf",
      "quants/RhizStol_rep1/quant.sf", "quants/RhizStol_rep2/quant.sf", "quants/RhizStol_rep3/quant.sf"
    )
    
    names(files) <- c(
      "AutoBud_1", "AutoBud_2", "AutoBud_3",
      "AutoMat_1", "AutoMat_2", "AutoMat_3",
      "AvicBud_1", "AvicBud_2", "AvicBud_3",
      "AvicMat_1", "AvicMat_2", "AvicMat_3",
      "RhizAuto_1", "RhizAuto_2", "RhizAuto_3",
      "RhizStol_1", "RhizStol_2", "RhizStol_3"
    )

# Import
    txi <- tximport(files, type = "salmon", txOut = TRUE)

# Metadata
    tissue <- factor(rep(c("AutoBud", "AutoMat", "AvicBud", "AvicMat", "RhizAuto", "RhizStol"), each = 3))
    rep <- factor(rep(1:3, 6))
    samples <- data.frame(row.names = names(files), tissue = tissue, rep = rep)

# DESeq2
    dds <- DESeqDataSetFromTximport(txi, colData = samples, design = ~ tissue)

# Filter low counts
    keep <- rowSums(counts(dds) >= 10) >= 3
    dds <- dds[keep,]

# Run DESeq2
    dds <- DESeq(dds)

# VST transformation
    vsd <- vst(dds, blind = FALSE)
    norm_counts <- assay(vsd)

# Save
    save(txi, dds, vsd, norm_counts, samples, file = "bugulina_expression.RData")

# How many transcripts retained?
    cat("Transcripts after filtering:", nrow(dds), "\n")
    library(ggrepel)
    library(ggplot2)

# Run PCA
    pca <- plotPCA(vsd, intgroup = "tissue", returnData = TRUE)
    percentVar <- round(100 * attr(pca, "percentVar"))
    
    ggplot(pca, aes(PC1, PC2, color = tissue, label = name)) +
      geom_point(size = 4) +
      geom_text_repel(size = 3, show.legend = FALSE) +
      xlab(paste0("PC1: ", percentVar[1], "% variance")) +
      ylab(paste0("PC2: ", percentVar[2], "% variance")) +
      ggtitle("Bugulina stolonifera - Tissue PCA") +
      theme_minimal()
<img width="1078" height="1019" alt="image" src="https://github.com/user-attachments/assets/44e295f6-17cb-47ad-9403-de2324de914d" />

    library(pheatmap)
    library(RColorBrewer)
    
    sampleDists <- dist(t(assay(vsd)))
    sampleDistMatrix <- as.matrix(sampleDists)
    colors <- colorRampPalette(rev(brewer.pal(9, "Blues")))(255)
    
    pheatmap(sampleDistMatrix,
             clustering_distance_rows = sampleDists,
             clustering_distance_cols = sampleDists,
             col = colors,
             main = "Sample Distance Heatmap")

<img width="1078" height="1019" alt="image" src="https://github.com/user-attachments/assets/cc27ad13-5ed1-4cea-93d9-10e6b454ceab" />

# Get results
    res_AutoMat_vs_AutoBud <- results(dds, contrast = c("tissue", "AutoMat", "AutoBud"), alpha = 0.05)
    summary(res_AutoMat_vs_AutoBud)

# Order by significance
    res_AutoMat_vs_AutoBud <- res_AutoMat_vs_AutoBud[order(res_AutoMat_vs_AutoBud$padj),]

    out of 62577 with nonzero total read count
    adjusted p-value < 0.05
    LFC > 0 (up)       : 376, 0.6%
    LFC < 0 (down)     : 241, 0.39%
    outliers [1]       : 2305, 3.7%
    low counts [2]     : 13075, 21%
    (mean count < 6)
    [1] see 'cooksCutoff' argument of ?results
    [2] see 'independentFiltering' argument of ?results
# Top 20 genes
    head(res_AutoMat_vs_AutoBud, 20)
            log2 fold change (MLE): tissue AutoMat vs AutoBud 
            Wald test p-value: tissue AutoMat vs AutoBud 
            DataFrame with 20 rows and 6 columns
                                        baseMean log2FoldChange     lfcSE      stat      pvalue        padj
                                       <numeric>      <numeric> <numeric> <numeric>   <numeric>   <numeric>
            TRINITY_DN137987_c68_g1_i1 6568.8777       -27.7938   2.28032 -12.18853 3.57816e-34 1.68878e-29
            TRINITY_DN127001_c1_g1_i2    74.4939       -22.1682   2.23610  -9.91380 3.62601e-23 8.55685e-19
            TRINITY_DN130256_c0_g1_i4    84.6336        19.4224   2.04106   9.51587 1.80203e-21 2.83501e-17
            TRINITY_DN139431_c0_g1_i4   308.9888        18.8242   2.13920   8.79964 1.37258e-18 1.29564e-14
            TRINITY_DN135224_c0_g1_i2    79.9359       -22.7416   2.57967  -8.81570 1.18936e-18 1.29564e-14
            ...                              ...            ...       ...       ...         ...         ...
            TRINITY_DN134747_c1_g1_i3    75.4029       -22.5941   3.01639  -7.49044 6.86413e-14 2.02479e-10
            TRINITY_DN130497_c0_g1_i1    72.7906       -21.8953   2.96526  -7.38393 1.53681e-13 4.02960e-10
            TRINITY_DN141702_c0_g2_i2    79.8529       -22.7161   3.07535  -7.38653 1.50713e-13 4.02960e-10
            TRINITY_DN130133_c0_g1_i6    66.6083       -22.0426   2.99346  -7.36358 1.79041e-13 4.44747e-10
            TRINITY_DN135518_c0_g1_i1   182.5512       -23.4878   3.19350  -7.35489 1.91080e-13 4.50919e-10
> # Get results
# Volcano plot
    library(ggrepel)
    
    res_df <- as.data.frame(res_AutoMat_vs_AutoBud)
    res_df$gene <- rownames(res_df)
    res_df$sig <- ifelse(res_df$padj < 0.05 & abs(res_df$log2FoldChange) > 1, "Sig", "NS")
    res_df$sig[is.na(res_df$sig)] <- "NS"
    
    ggplot(res_df, aes(log2FoldChange, -log10(padj), color = sig)) +
      geom_point(size = 0.5, alpha = 0.6) +
      scale_color_manual(values = c("grey70", "red")) +
      geom_vline(xintercept = c(-1, 1), linetype = "dashed", alpha = 0.3) +
      geom_hline(yintercept = -log10(0.05), linetype = "dashed", alpha = 0.3) +
      ggtitle("AutoMat vs AutoBud") +
      theme_minimal()

<img width="1078" height="1019" alt="image" src="https://github.com/user-attachments/assets/a49b3656-12ce-4a30-9594-1a3c2c886894" />


