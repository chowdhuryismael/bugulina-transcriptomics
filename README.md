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






# Top 500 most variable genes
    topVarGenes <- head(order(rowVars(norm_counts), decreasing = TRUE), 500)
    heatmap_data <- norm_counts[topVarGenes, ]

# Create annotation for tissues
    ann_col <- data.frame(tissue = samples$tissue)
    rownames(ann_col) <- colnames(heatmap_data)

# Color palette
    tissue_colors <- c("AutoBud" = "#E41A1C", "AutoMat" = "#377EB8", 
                       "AvicBud" = "#4DAF4A", "AvicMat" = "#984EA3",
                       "RhizAuto" = "#FF7F00", "RhizStol" = "#A65628")
    ann_colors <- list(tissue = tissue_colors)

    pheatmap(heatmap_data, 
             annotation_col = ann_col,
             annotation_colors = ann_colors,
             show_rownames = FALSE,
             scale = "row",
             clustering_distance_cols = "correlation",
             main = "Top 500 Variable Genes Across Tissues")


<img width="1078" height="1019" alt="image" src="https://github.com/user-attachments/assets/49a131cc-60f8-4910-bc57-37eff9f74b52" />


# Define comparisons of interest
    comparisons <- list(
      c("AutoMat", "AutoBud"),   # Mature vs bud autozooid
      c("AvicMat", "AvicBud"),   # Mature vs bud avicularium
      c("AvicBud", "AutoBud"),   # Avicularium vs autozooid bud
      c("AvicMat", "AutoMat"),   # Mature avicularium vs mature autozooid
      c("RhizAuto", "RhizStol"), # Rhizoid autozooid vs network
      c("RhizAuto", "AutoMat"),  # Rhizoid vs autozooid (mature)
      c("RhizStol", "AutoBud")   # Stolon network vs autozooid bud
    )

# Run all comparisons
        degs_list <- list()
        for(comp in comparisons) {
          name <- paste0(comp[1], "_vs_", comp[2])
          cat("\n=== ", name, " ===\n")
          res <- results(dds, contrast = c("tissue", comp[1], comp[2]), alpha = 0.05)
          summary(res)
          degs_list[[name]] <- res
        }
        
        ===  AutoMat_vs_AutoBud  ===
        
        out of 62577 with nonzero total read count
        adjusted p-value < 0.05
        LFC > 0 (up)       : 376, 0.6%
        LFC < 0 (down)     : 241, 0.39%
        outliers [1]       : 2305, 3.7%
        low counts [2]     : 13075, 21%
        (mean count < 6)
        [1] see 'cooksCutoff' argument of ?results
        [2] see 'independentFiltering' argument of ?results
        
        
        ===  AvicMat_vs_AvicBud  ===
        
        out of 62577 with nonzero total read count
        adjusted p-value < 0.05
        LFC > 0 (up)       : 1049, 1.7%
        LFC < 0 (down)     : 375, 0.6%
        outliers [1]       : 2305, 3.7%
        low counts [2]     : 11914, 19%
        (mean count < 6)
        [1] see 'cooksCutoff' argument of ?results
        [2] see 'independentFiltering' argument of ?results
        
        
        ===  AvicBud_vs_AutoBud  ===
        
        out of 62577 with nonzero total read count
        adjusted p-value < 0.05
        LFC > 0 (up)       : 2235, 3.6%
        LFC < 0 (down)     : 3246, 5.2%
        outliers [1]       : 2305, 3.7%
        low counts [2]     : 7183, 11%
        (mean count < 5)
        [1] see 'cooksCutoff' argument of ?results
        [2] see 'independentFiltering' argument of ?results
        
        
        ===  AvicMat_vs_AutoMat  ===
        
        out of 62577 with nonzero total read count
        adjusted p-value < 0.05
        LFC > 0 (up)       : 1863, 3%
        LFC < 0 (down)     : 1583, 2.5%
        outliers [1]       : 2305, 3.7%
        low counts [2]     : 11914, 19%
        (mean count < 6)
        [1] see 'cooksCutoff' argument of ?results
        [2] see 'independentFiltering' argument of ?results
        
        
        ===  RhizAuto_vs_RhizStol  ===
        
        out of 62577 with nonzero total read count
        adjusted p-value < 0.05
        LFC > 0 (up)       : 997, 1.6%
        LFC < 0 (down)     : 438, 0.7%
        outliers [1]       : 2305, 3.7%
        low counts [2]     : 21220, 34%
        (mean count < 10)
        [1] see 'cooksCutoff' argument of ?results
        [2] see 'independentFiltering' argument of ?results
        
        
        ===  RhizAuto_vs_AutoMat  ===
        
        out of 62577 with nonzero total read count
        adjusted p-value < 0.05
        LFC > 0 (up)       : 303, 0.48%
        LFC < 0 (down)     : 296, 0.47%
        outliers [1]       : 2305, 3.7%
        low counts [2]     : 9556, 15%
        (mean count < 5)
        [1] see 'cooksCutoff' argument of ?results
        [2] see 'independentFiltering' argument of ?results
        
        
        ===  RhizStol_vs_AutoBud  ===
        
        out of 62577 with nonzero total read count
        adjusted p-value < 0.05
        LFC > 0 (up)       : 1972, 3.2%
        LFC < 0 (down)     : 2080, 3.3%
        outliers [1]       : 2305, 3.7%
        low counts [2]     : 20071, 32%
        (mean count < 9)
        [1] see 'cooksCutoff' argument of ?results
        [2] see 'independentFiltering' argument of ?results

 Count DEGs per comparison
 
        deg_counts <- sapply(degs_list, function(x) {
          sum(x$padj < 0.05, na.rm = TRUE)
        })
        print(deg_counts)

         AutoMat_vs_AutoBud   AvicMat_vs_AvicBud   AvicBud_vs_AutoBud   AvicMat_vs_AutoMat RhizAuto_vs_RhizStol  RhizAuto_vs_AutoMat  RhizStol_vs_AutoBud 
                 617                 1424                 5481                 3446                 1435                  599                 4052 


# Function to get top DEGs

        get_top_degs <- function(res, n = 10) {
          res_sig <- res[which(res$padj < 0.05), ]
          res_sig <- res_sig[order(res_sig$padj), ]
          head(res_sig, n)
        }
        
        for(name in names(degs_list)) {
          cat("\n=== Top 10 DEGs:", name, "===\n")
          print(get_top_degs(degs_list[[name]]))
        }

    === Top 10 DEGs: AutoMat_vs_AutoBud ===
    log2 fold change (MLE): tissue AutoMat vs AutoBud 
    Wald test p-value: tissue AutoMat vs AutoBud 
    DataFrame with 10 rows and 6 columns
                                baseMean log2FoldChange     lfcSE      stat      pvalue        padj
                               <numeric>      <numeric> <numeric> <numeric>   <numeric>   <numeric>
    TRINITY_DN137987_c68_g1_i1 6568.8777       -27.7938   2.28032 -12.18853 3.57816e-34 1.68878e-29
    TRINITY_DN127001_c1_g1_i2    74.4939       -22.1682   2.23610  -9.91380 3.62601e-23 8.55685e-19
    TRINITY_DN130256_c0_g1_i4    84.6336        19.4224   2.04106   9.51587 1.80203e-21 2.83501e-17
    TRINITY_DN139431_c0_g1_i4   308.9888        18.8242   2.13920   8.79964 1.37258e-18 1.29564e-14
    TRINITY_DN135224_c0_g1_i2    79.9359       -22.7416   2.57967  -8.81570 1.18936e-18 1.29564e-14
    TRINITY_DN121618_c0_g2_i1   348.1720        22.8416   2.68466   8.50818 1.76680e-17 1.38980e-13
    TRINITY_DN134375_c0_g1_i4    63.3538       -21.8890   2.60729  -8.39531 4.64673e-17 3.13302e-13
    TRINITY_DN138304_c3_g9_i3   317.4491       -23.5198   2.84155  -8.27711 1.26196e-16 7.44506e-13
    TRINITY_DN136236_c0_g1_i4   133.1017       -21.6705   2.64045  -8.20712 2.26550e-16 1.18805e-12
    TRINITY_DN126754_c2_g3_i6   345.5373       -22.0694   2.72167  -8.10878 5.11301e-16 2.41319e-12
    
    === Top 10 DEGs: AvicMat_vs_AvicBud ===
    log2 fold change (MLE): tissue AvicMat vs AvicBud 
    Wald test p-value: tissue AvicMat vs AvicBud 
    DataFrame with 10 rows and 6 columns
                                 baseMean log2FoldChange     lfcSE      stat      pvalue        padj
                                <numeric>      <numeric> <numeric> <numeric>   <numeric>   <numeric>
    TRINITY_DN135455_c0_g1_i3     33.8364       -38.4312   2.59843  -14.7902 1.69554e-49 8.19928e-45
    TRINITY_DN139859_c1_g2_i3     39.5060       -44.1889   3.41950  -12.9226 3.35577e-38 8.11392e-34
    TRINITY_DN132903_c0_g1_i1    442.7861        22.9079   2.02288   11.3244 9.93559e-30 1.60155e-25
    TRINITY_DN137955_c29_g13_i1 2889.5436       -32.2645   2.86996  -11.2421 2.53186e-29 3.06090e-25
    TRINITY_DN39367_c0_g1_i1      58.9145        34.9907   3.13437   11.1635 6.14890e-29 5.94697e-25
    TRINITY_DN139710_c0_g1_i2     11.8856        35.8363   3.30147   10.8546 1.89542e-27 1.52765e-23
    TRINITY_DN122384_c0_g1_i1     24.7274       -39.2116   3.64786  -10.7492 5.97678e-27 4.12893e-23
    TRINITY_DN141113_c94_g1_i4   488.6467       -24.3020   2.28101  -10.6541 1.66867e-26 1.00867e-22
    TRINITY_DN135729_c0_g15_i1    53.5098        31.1131   2.95935   10.5135 7.48458e-26 4.02155e-22
    TRINITY_DN136494_c0_g1_i1    223.1051        25.1957   2.42491   10.3904 2.74327e-25 1.32659e-21
    
    === Top 10 DEGs: AvicBud_vs_AutoBud ===
    log2 fold change (MLE): tissue AvicBud vs AutoBud 
    Wald test p-value: tissue AvicBud vs AutoBud 
    DataFrame with 10 rows and 6 columns
                               baseMean log2FoldChange     lfcSE      stat      pvalue        padj
                              <numeric>      <numeric> <numeric> <numeric>   <numeric>   <numeric>
    TRINITY_DN132903_c0_g1_i1  442.7861       -26.0666   2.02167 -12.89360 4.89094e-38 2.59655e-33
    TRINITY_DN123077_c0_g1_i1  231.6966       -25.0143   2.21242 -11.30631 1.22113e-29 3.24142e-25
    TRINITY_DN140012_c0_g1_i3   99.8759       -24.3097   2.29156 -10.60838 2.72445e-26 4.82128e-22
    TRINITY_DN132652_c3_g1_i3 2844.1628       -28.6733   2.71427 -10.56390 4.38063e-26 5.81409e-22
    TRINITY_DN136494_c0_g1_i1  223.1051       -25.1358   2.42518 -10.36448 3.59711e-25 3.81934e-21
    TRINITY_DN137605_c1_g1_i1   75.8437       -23.4059   2.29028 -10.21968 1.61879e-24 1.43233e-20
    TRINITY_DN138873_c1_g2_i2  152.0283       -26.0804   2.57501 -10.12825 4.14010e-24 3.13991e-20
    TRINITY_DN115876_c0_g1_i2  101.0599       -22.5402   2.26180  -9.96561 2.15557e-23 1.43046e-19
    TRINITY_DN133750_c0_g2_i2  133.2403       -24.4851   2.48810  -9.84087 7.50561e-23 4.42739e-19
    TRINITY_DN142492_c0_g3_i5   38.0734       -22.4959   2.32210  -9.68777 3.39860e-22 1.80428e-18
    
    === Top 10 DEGs: AvicMat_vs_AutoMat ===
    log2 fold change (MLE): tissue AvicMat vs AutoMat 
    Wald test p-value: tissue AvicMat vs AutoMat 
    DataFrame with 10 rows and 6 columns
                                 baseMean log2FoldChange     lfcSE      stat      pvalue        padj
                                <numeric>      <numeric> <numeric> <numeric>   <numeric>   <numeric>
    TRINITY_DN139736_c2_g5_i1     40.1107        41.6587   2.72000   15.3157 6.00706e-53 2.90490e-48
    TRINITY_DN139731_c0_g1_i8     75.6007        47.5070   3.14072   15.1262 1.08850e-51 2.63189e-47
    TRINITY_DN135455_c0_g1_i3     33.8364       -38.6790   2.59816  -14.8870 4.00096e-50 6.44928e-46
    TRINITY_DN140223_c0_g1_i6     22.0807        40.1949   3.14478   12.7815 2.08105e-37 2.51589e-33
    TRINITY_DN139859_c1_g2_i3     39.5060       -43.3112   3.42016  -12.6635 9.42064e-37 9.11126e-33
    TRINITY_DN112378_c0_g4_i1     20.3833        43.7177   3.53317   12.3735 3.63589e-35 2.93041e-31
    TRINITY_DN39949_c0_g1_i1      18.7365        41.1756   3.38357   12.1693 4.53106e-34 3.13019e-30
    TRINITY_DN137955_c29_g13_i1 2889.5436       -33.6310   2.86763  -11.7278 9.17912e-32 5.54855e-28
    TRINITY_DN107198_c0_g1_i1     17.6699        37.6499   3.26654   11.5259 9.76788e-31 4.72355e-27
    TRINITY_DN137987_c68_g1_i1  6568.8777        26.3012   2.28036   11.5338 8.91390e-31 4.72355e-27
    
    === Top 10 DEGs: RhizAuto_vs_RhizStol ===
    log2 fold change (MLE): tissue RhizAuto vs RhizStol 
    Wald test p-value: tissue RhizAuto vs RhizStol 
    DataFrame with 10 rows and 6 columns
                               baseMean log2FoldChange     lfcSE      stat      pvalue        padj
                              <numeric>      <numeric> <numeric> <numeric>   <numeric>   <numeric>
    TRINITY_DN142083_c0_g1_i7   35.5514       -46.1626   3.25076 -14.20055 9.08898e-46 3.54943e-41
    TRINITY_DN135091_c0_g1_i1   17.4948       -37.0624   3.24326 -11.42751 3.04718e-30 5.94992e-26
    TRINITY_DN141961_c0_g4_i1  121.6115        22.9770   2.04267  11.24850 2.35569e-29 3.03573e-25
    TRINITY_DN113391_c0_g2_i1   22.4504       -33.4442   2.97970 -11.22398 3.10942e-29 3.03573e-25
    TRINITY_DN141319_c1_g1_i3  131.9972        39.3256   3.56076  11.04417 2.33929e-28 1.82708e-24
    TRINITY_DN136325_c0_g1_i1  100.1108        22.7468   2.06660  11.00687 3.54074e-28 2.30455e-24
    TRINITY_DN138279_c1_g1_i1  145.2186        23.3245   2.17290  10.73425 7.02848e-27 3.92109e-23
    TRINITY_DN140366_c0_g1_i4  110.1083       -38.6991   3.70622 -10.44166 1.59981e-25 7.80948e-22
    TRINITY_DN98678_c0_g1_i3    15.2677        37.7074   3.62397  10.40499 2.35293e-25 1.02096e-21
    TRINITY_DN139617_c0_g1_i1   16.0461        36.6655   3.74573   9.78861 1.26017e-22 4.92120e-19
    
    === Top 10 DEGs: RhizAuto_vs_AutoMat ===
    log2 fold change (MLE): tissue RhizAuto vs AutoMat 
    Wald test p-value: tissue RhizAuto vs AutoMat 
    DataFrame with 10 rows and 6 columns
                                baseMean log2FoldChange     lfcSE      stat      pvalue        padj
                               <numeric>      <numeric> <numeric> <numeric>   <numeric>   <numeric>
    TRINITY_DN139736_c2_g5_i1    40.1107        41.9077   2.72024   15.4059 1.49450e-53 7.57951e-49
    TRINITY_DN139731_c0_g1_i8    75.6007        44.2633   3.14545   14.0721 5.63352e-45 1.42855e-40
    TRINITY_DN142083_c0_g1_i7    35.5514       -44.3929   3.25185  -13.6516 1.97517e-42 3.33909e-38
    TRINITY_DN137987_c68_g1_i1 6568.8777        29.1586   2.28028   12.7873 1.93081e-37 2.44807e-33
    TRINITY_DN140223_c0_g1_i6    22.0807        39.5910   3.14710   12.5801 2.71608e-36 2.75497e-32
    TRINITY_DN135729_c0_g8_i2    16.5672        38.2991   3.45428   11.0874 1.44383e-28 1.22042e-24
    TRINITY_DN135091_c0_g1_i1    17.4948       -35.6528   3.24591  -10.9839 4.56777e-28 3.30941e-24
    TRINITY_DN112378_c0_g4_i1    20.3833        38.4128   3.58919   10.7024 9.92137e-27 6.28966e-23
    TRINITY_DN141397_c1_g2_i4    55.1188        40.9545   3.91707   10.4554 1.38391e-25 7.79851e-22
    TRINITY_DN133750_c0_g1_i1  1696.9042       -29.9030   2.94884  -10.1406 3.64856e-24 1.85040e-20
    
    === Top 10 DEGs: RhizStol_vs_AutoBud ===
    log2 fold change (MLE): tissue RhizStol vs AutoBud 
    Wald test p-value: tissue RhizStol vs AutoBud 
    DataFrame with 10 rows and 6 columns
                               baseMean log2FoldChange     lfcSE      stat      pvalue        padj
                              <numeric>      <numeric> <numeric> <numeric>   <numeric>   <numeric>
    TRINITY_DN139431_c0_g1_i4  308.9888        24.5316  2.134840  11.49106 1.46302e-30 5.88148e-26
    TRINITY_DN124546_c2_g3_i1 9630.6788        11.1805  1.004104  11.13480 8.49343e-29 1.70722e-24
    TRINITY_DN141961_c0_g4_i1  121.6115       -22.4491  2.043681 -10.98465 4.52998e-28 6.07033e-24
    TRINITY_DN138279_c1_g1_i1  145.2186       -23.4576  2.173112 -10.79445 3.65636e-27 3.32420e-23
    TRINITY_DN136325_c0_g1_i1  100.1108       -22.2957  2.067638 -10.78316 4.13447e-27 3.32420e-23
    TRINITY_DN130256_c0_g1_i4   84.6336        21.2654  2.039840  10.42502 1.90611e-25 1.27713e-21
    TRINITY_DN32905_c0_g1_i1  1277.2202       -27.3083  2.683265 -10.17727 2.50484e-24 1.43853e-20
    TRINITY_DN132836_c0_g1_i1  482.6230         6.2953  0.623064  10.10376 5.31614e-24 2.67143e-20
    TRINITY_DN132948_c0_g1_i3  103.6418       -22.9194  2.341395  -9.78877 1.25817e-22 5.61997e-19
    TRINITY_DN133242_c0_g1_i2   23.1153       -20.0692  2.078958  -9.65348 4.75147e-22 1.73649e-18
    > 

 
 # Install UpSetR if needed
    install.packages("UpSetR")
    library(UpSetR)

# Create binary matrix of DEGs per comparison
    all_degs <- unique(unlist(lapply(degs_list, function(res) {
      rownames(res[which(res$padj < 0.05), ])
    })))
    
    deg_matrix <- data.frame(row.names = all_degs)
    for(name in names(degs_list)) {
      res <- degs_list[[name]]
      sig <- rownames(res[which(res$padj < 0.05), ])
      deg_matrix[, name] <- as.integer(all_degs %in% sig)
    }
    
    upset(deg_matrix, sets = names(deg_matrix), 
          order.by = "freq", 
          main.bar.color = "steelblue",
          sets.bar.color = "firebrick")
            
<img width="1078" height="1019" alt="image" src="https://github.com/user-attachments/assets/cd16cfab-c2a9-4a69-b527-29ac54760785" />



# Get top 20 DEGs from each comparison
top_genes <- unique(unlist(lapply(degs_list, function(res) {
  sig <- res[which(res$padj < 0.05), ]
  sig <- sig[order(sig$padj), ]
  rownames(sig)[1:20]
})))

cat("Plotting", length(top_genes), "genes\n")

# Heatmap of these genes across all samples
heatmap_top <- norm_counts[top_genes, ]
pheatmap(heatmap_top, 
         annotation_col = ann_col,
         annotation_colors = ann_colors,
         show_rownames = FALSE,
         scale = "row",
         clustering_distance_cols = "correlation",
         main = "Top DEGs Across All Tissue Comparisons",
         fontsize = 8)

<img width="1078" height="1019" alt="image" src="https://github.com/user-attachments/assets/5cf2e07e-8272-4e6d-b5ec-de7e03d5e11f" />





____________________________________________________________________________________________________
####################################################################################################
____________________________________________________________________________________________________

## Annoatation

## Transdecoder
        TransDecoder.LongOrfs \                                                                                                                                                         
                -t top_DEGs_seqs.fasta \
                 -m 50 \
                 -O transdecoder_results \
                 -G Universal

        TransDecoder.Predict \                                                                                                                                                       
                            -t top_DEGs_seqs.fasta \
                             --output_dir transdecoder_results \
                             --single_best_only



### Blast
diamond blastx \
    --db /projects/health_sciences/bms/biochemistry/kenny_group/katerinaachilleos/Databases/uniprot/reference_proteomes.dmnd \
    --query top_DEGs_seqs.fasta \
    --out diamond_results/top_DEGs_diamond.txt \
    --outfmt 6 qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore stitle \
    --threads 16 \
    --max-target-seqs 5 \
    --evalue 1e-5 \
    --sensitive

    
for fasta in *.fasta
    set name (basename $fasta .fasta)
    echo "Diamond on $name..."
    diamond blastx \
        --db /projects/health_sciences/bms/biochemistry/kenny_group/katerinaachilleos/Databases/uniprot/reference_proteomes.dmnd \
        --query $fasta \
        --out diamond_results/$name\_diamond.txt \
        --outfmt 6 qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore stitle \
        --threads 8 \
        --max-target-seqs 5 \
        --evalue 1e-5 \
        --sensitive &
end
wait
echo "All Diamond runs complete!"

