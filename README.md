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

# 1A: Load expression data and get tissue-level summaries
        
       Total transcripts with expression: 62577 
> # Top 500 expressed in each tissue
        > top500_per_tissue <- list()
        > for(tissue in colnames(tissue_means)) {
        +   top500_per_tissue[[tissue]] <- head(order(tissue_means[, tissue], decreasing = TRUE), 500)
        + }
        > # Top 500 most highly expressed overall (mean across tissues)
        > tissue_means$overall_mean <- rowMeans(tissue_means[, 1:6])
        > top500_overall <- head(order(tissue_means$overall_mean, decreasing = TRUE), 500)
        > # Shared across all tissues
        > shared_all <- rowSums(expressed) == 6
        Error in h(simpleError(msg, call)) : 
          error in evaluating the argument 'x' in selecting a method for function 'rowSums': object 'expressed' not found
        
        > # 1B: Find unique genes per tissue
        > # Define "expressed" as mean normalized count > 10
        > expressed <- tissue_means[, 1:6] > 10
        > # Unique to each tissue (only in that tissue, not in others)
        > unique_genes <- list()
        > for(tissue in colnames(expressed)) {
        +   only_this <- expressed[, tissue] & rowSums(expressed[, colnames(expressed) != tissue]) == 0
        +   unique_genes[[tissue]] <- rownames(expressed)[only_this]
        +   cat(tissue, ":", sum(only_this), "unique genes\n")
        + }
        AutoBud : 44 unique genes
        AutoMat : 220 unique genes
        AvicBud : 143 unique genes
        AvicMat : 80 unique genes
        RhizAuto : 16 unique genes
        RhizStol : 266 unique genes
        > # Shared across all tissues
        > shared_all <- rowSums(expressed) == 6
        > cat("Shared across all tissues:", sum(shared_all), "genes\n")
        Shared across all tissues: 347 genes
        > # Shared between specific pairs/comparisons
        > # Autozooid vs Avicularium (bud stage)
        > auto_bud_avic_bud_shared <- expressed[, "AutoBud"] & expressed[, "AvicBud"]
        > cat("Shared: AutoBud & AvicBud:", sum(auto_bud_avic_bud_shared), "\n")
        Shared: AutoBud & AvicBud: 522 
        > 
        > 
        > # Pairwise shared genes
        > cat("\n=== Pairwise shared genes ===\n")
        
        === Pairwise shared genes ===
        > tissues <- colnames(expressed)
        > pairwise_shared <- matrix(0, 6, 6, dimnames = list(tissues, tissues))
        > for(i in 1:6) {
        +   for(j in 1:6) {
        +     shared <- expressed[, i] & expressed[, j]
        +     pairwise_shared[i, j] <- sum(shared)
        +   }
        + }
        > print(pairwise_shared)
                 AutoBud AutoMat AvicBud AvicMat RhizAuto RhizStol
        AutoBud      831     636     522     573      647      470
        AutoMat      636     994     470     540      651      469
        AvicBud      522     470     940     681      529      552
        AvicMat      573     540     681     904      581      520
        RhizAuto     647     651     529     581      808      521
        RhizStol     470     469     552     520      521      966
        > # Jaccard similarity (shared / union)
        > cat("\n=== Jaccard similarity (shared/union) ===\n")
        
        === Jaccard similarity (shared/union) ===
        > jaccard <- matrix(0, 6, 6, dimnames = list(tissues, tissues))
        > for(i in 1:6) {
        +   for(j in 1:6) {
        +     union <- expressed[, i] | expressed[, j]
        +     shared <- expressed[, i] & expressed[, j]
        +     jaccard[i, j] <- round(sum(shared) / sum(union), 3)
        +   }
        + }
        > print(jaccard)
                 AutoBud AutoMat AvicBud AvicMat RhizAuto RhizStol
        AutoBud    1.000   0.535   0.418   0.493    0.652    0.354
        AutoMat    0.535   1.000   0.321   0.398    0.566    0.315
        AvicBud    0.418   0.321   1.000   0.586    0.434    0.408
        AvicMat    0.493   0.398   0.586   1.000    0.514    0.385
        RhizAuto   0.652   0.566   0.434   0.514    1.000    0.416
        RhizStol   0.354   0.315   0.408   0.385    0.416    1.000
        > # Specific pairwise comparisons of interest
        > cat("\n=== Key biological comparisons ===\n")
        
        === Key biological comparisons ===
        > # Buds: autozooid vs avicularium
        > shared_buds <- expressed[, "AutoBud"] & expressed[, "AvicBud"]
        > cat("Shared AutoBud & AvicBud:", sum(shared_buds), 
        +     "(Jaccard:", round(sum(shared_buds)/sum(expressed[, "AutoBud"] | expressed[, "AvicBud"]), 3), ")\n")
        Shared AutoBud & AvicBud: 522 (Jaccard: 0.418 )
        > # Mature: autozooid vs avicularium
        > shared_mature <- expressed[, "AutoMat"] & expressed[, "AvicMat"]
        > cat("Shared AutoMat & AvicMat:", sum(shared_mature),
        +     "(Jaccard:", round(sum(shared_mature)/sum(expressed[, "AutoMat"] | expressed[, "AvicMat"]), 3), ")\n")
        Shared AutoMat & AvicMat: 540 (Jaccard: 0.398 )
        > # Autozooid: bud vs mature
        > shared_auto <- expressed[, "AutoBud"] & expressed[, "AutoMat"]
        > cat("Shared AutoBud & AutoMat:", sum(shared_auto),
        +     "(Jaccard:", round(sum(shared_auto)/sum(expressed[, "AutoBud"] | expressed[, "AutoMat"]), 3), ")\n")
        Shared AutoBud & AutoMat: 636 (Jaccard: 0.535 )
        > # Avicularium: bud vs mature
        > shared_avic <- expressed[, "AvicBud"] & expressed[, "AvicMat"]
        > cat("Shared AvicBud & AvicMat:", sum(shared_avic),
        +     "(Jaccard:", round(sum(shared_avic)/sum(expressed[, "AvicBud"] | expressed[, "AvicMat"]), 3), ")\n")
        Shared AvicBud & AvicMat: 681 (Jaccard: 0.586 )
        > # Rhizoid: autozooid vs network
        > shared_rhiz <- expressed[, "RhizAuto"] & expressed[, "RhizStol"]
        > cat("Shared RhizAuto & RhizStol:", sum(shared_rhiz),
        +     "(Jaccard:", round(sum(shared_rhiz)/sum(expressed[, "RhizAuto"] | expressed[, "RhizStol"]), 3), ")\n")
        Shared RhizAuto & RhizStol: 521 (Jaccard: 0.416 )
        > # AutoMat vs RhizAuto (both mature, both feeding-related?)
        > shared_mat_rhiz <- expressed[, "AutoMat"] & expressed[, "RhizAuto"]
        > cat("Shared AutoMat & RhizAuto:", sum(shared_mat_rhiz),
        +     "(Jaccard:", round(sum(shared_mat_rhiz)/sum(expressed[, "AutoMat"] | expressed[, "RhizAuto"]), 3), ")\n")
        Shared AutoMat & RhizAuto: 651 (Jaccard: 0.566 )
        > # AvicMat vs RhizStol (structural/defensive?)
        > shared_avic_rhiz <- expressed[, "AvicMat"] & expressed[, "RhizStol"]
        > cat("Shared AvicMat & RhizStol:", sum(shared_avic_rhiz),
        +     "(Jaccard:", round(sum(shared_avic_rhiz)/sum(expressed[, "AvicMat"] | expressed[, "RhizStol"]), 3), ")\n")
        Shared AvicMat & RhizStol: 520 (Jaccard: 0.385 )
        > # AutoBud vs RhizStol (budding/growing tissues)
        > shared_growing <- expressed[, "AutoBud"] & expressed[, "RhizStol"]
        > cat("Shared AutoBud & RhizStol:", sum(shared_growing),
        +     "(Jaccard:", round(sum(shared_growing)/sum(expressed[, "AutoBud"] | expressed[, "RhizStol"]), 3), ")\n")
        Shared AutoBud & RhizStol: 470 (Jaccard: 0.354 )
        > # Venn diagram data for key trios
        > cat("\n=== Triple overlaps ===\n")
        
        === Triple overlaps ===
        > # Buds + mature autozooids
        > tri_auto <- expressed[, "AutoBud"] & expressed[, "AutoMat"] & expressed[, "AvicBud"]
        > cat("Shared AutoBud + AutoMat + AvicBud:", sum(tri_auto), "\n")
        Shared AutoBud + AutoMat + AvicBud: 428 
        > # Mature tissues
        > tri_mature <- expressed[, "AutoMat"] & expressed[, "AvicMat"] & expressed[, "RhizAuto"]
        > cat("Shared AutoMat + AvicMat + RhizAuto:", sum(tri_mature), "\n")
        Shared AutoMat + AvicMat + RhizAuto: 498 
        > # Rhizoid types + autozooid mature
        > tri_rhiz <- expressed[, "RhizAuto"] & expressed[, "RhizStol"] & expressed[, "AutoMat"]
        > cat("Shared RhizAuto + RhizStol + AutoMat:", sum(tri_rhiz), "\n")
        Shared RhizAuto + RhizStol + AutoMat: 427 
        > # Save all results
        > save(expressed, unique_genes, shared_all, pairwise_shared, jaccard,
        +      file = "tissue_overlap_analysis.RData")
        > # Number of genes per tissue
        > cat("\n=== Genes expressed per tissue (>10 normalized counts) ===\n")
        
        === Genes expressed per tissue (>10 normalized counts) ===
        > for(tissue in colnames(expressed)) {
        +   cat(tissue, ":", sum(expressed[, tissue]), "\n")
        + }
        AutoBud : 831 
        AutoMat : 994 
        AvicBud : 940 
        AvicMat : 904 
        RhizAuto : 808 
        RhizStol : 966 
        > cat("\n=== Unique genes per tissue ===\n")
        
        === Unique genes per tissue ===
        > for(tissue in names(unique_genes)) {
        +   cat(tissue, ":", length(unique_genes[[tissue]]), "\n")
        + }
        AutoBud : 44 
        AutoMat : 220 
        AvicBud : 143 
        AvicMat : 80 
        RhizAuto : 16 
        RhizStol : 266 
        > cat("\n=== Shared across all 6 tissues:", sum(shared_all), "===\n")
        
        === Shared across all 6 tissues: 347 ===
        > # Overlap matrix
        > overlap_matrix <- crossprod(expressed[, 1:6] * 1)
        > print(overlap_matrix)
                 AutoBud AutoMat AvicBud AvicMat RhizAuto RhizStol
        AutoBud      831     636     522     573      647      470
        AutoMat      636     994     470     540      651      469
        AvicBud      522     470     940     681      529      552
        AvicMat      573     540     681     904      581      520
        RhizAuto     647     651     529     581      808      521
        RhizStol     470     469     552     520      521      966

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


# ══════════════════════════════════════════════════
# blast
# ══════════════════════════════════════════════════
    diamond blastx \
        --db /projects/health_sciences/bms/biochemistry/kenny_group/katerinaachilleos/Databases/uniprot/reference_proteomes.dmnd \
        --query top_DEGs_seqs.fasta \
        --out diamond_results/top_DEGs_diamond.txt \
        --outfmt 6 qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore stitle \
        --threads 16 \
        --max-target-seqs 5 \
        --evalue 1e-5 \
        --sensitive
        
    diamond blastx \                                                                                                                                                                             (blast_env) 
                                                                 --db $DIAMOND_DB \
                                                                 --query $FASTA \
                                                                 --out diamond_full_nt.txt \
                                                                 --outfmt 6 qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore stitle \
                                                                 --threads 32 \
                                                                 --max-target-seqs 1 \
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





    diamond blastp \                                                                                                                                                                          
                                                                 --db $DIAMOND_DB \
                                                                 --query Trinity_2019filtered_Reference.fasta.transdecoder.pep \
                                                                 --out diamond_full_prot.txt \
                                                                 --outfmt 6 qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore stitle \
                                                                 --threads 32 \
                                                                 --max-target-seqs 1 \
                                                                 --evalue 1e-5 \
                                                                 --sensitive
# ══════════════════════════════════════════════════
# interproscan
# ══════════════════════════════════════════════════
    
     set -x JAVA_TOOL_OPTIONS "-Xmx128G -Xms16G"                                                                                                                                         
                                                           interproscan.sh \
                                                                   -i Trinity_2019filtered_Reference.\
                                                           noSTOP.pep    -f tsv \
                                                                   -o interproscan_full.tsv \
                                                                   -cpu 32 \
                                                                   -goterms \
                                                                   -dp \
                                                                   -hm
# ══════════════════════════════════════════════════
# TransDecoder
# ══════════════════════════════════════════════════
    
    TransDecoder.LongOrfs \                                                                                                                                                                  
                                                                   -t top_DEGs_seqs.fasta \
                                                                   -m 50 \
                                                                   -O transdecoder_results \
                                                                   -G Universal
    
    
     TransDecoder.Predict \                                                                                                                                                                    
                                                                   -t top_DEGs_seqs.fasta \
                                                                   --output_dir transdecoder_results \
                                                                   --single_best_only


                                                               

# ══════════════════════════════════════════════════
# eggnog
# ══════════════════════════════════════════════════
    emapper.py \                                                                                                                                                                              
                                                                   -i Trinity_2019filtered_Reference.fasta.transdecoder.pep \
                                                                   --output full_transcriptome_eggnog \
                                                                   --cpu 32 \
                                                                   --itype proteins \
                                                                   --tax_scope Metazoa \
                                                                   --data_dir $EGGNOG_DB

#####################################################




################################
################################
    install.packages("clusterProfiler")
    install.packages("enrichplot")
    BiocManager::install("clusterProfiler")
    BiocManager::install("enrichplot")

a# ============================================
# ANNOTATION INTEGRATION & GO ENRICHMENT
# Run this after downloading HPC annotation files
# ============================================

    library(DESeq2)
    library(tximport)
    library(clusterProfiler)
    library(enrichplot)
    library(ggplot2)
    library(dplyr)
    library(tidyr)
    library(pheatmap)

# ============================================
# 1. LOAD ANNOTATIONS FROM HPC
# ============================================

# Check what files you actually have
    dir()
    list.files(pattern = "diamond")
    list.files(pattern = "eggnog")
    list.files(pattern = "interpro")
    list.files(pattern = "tabular")

# Check your working directory
    getwd()
    
    load("bugulina_expression.RData")
    load("tissue_specificity_analysis.RData")

# Diamond nucleotide results
    diamond_nt <- read.table("diamond_full_nt.txt", sep = "\t", stringsAsFactors = FALSE, quote = "")
    colnames(diamond_nt) <- c("transcript", "uniprot_id", "pident", "length", 
                              "mismatch", "gapopen", "qstart", "qend", 
                              "sstart", "send", "evalue", "bitscore", "description")

# Diamond protein results
    diamond_prot <- read.table("diamond_full_prot.txt", sep = "\t", stringsAsFactors = FALSE, quote = "")
    colnames(diamond_prot) <- c("transcript", "uniprot_id", "pident", "length",
                                "mismatch", "gapopen", "qstart", "qend",
                                "sstart", "send", "evalue", "bitscore", "description")

# eggNOG annotations
    eggnog <- read.table("full_transcriptome_eggnog.emapper.annotations",
                         sep = "\t", header = TRUE, stringsAsFactors = FALSE, 
                         quote = "", comment.char = "", na.strings = "-",
                         fill = TRUE, skip = 4)
# The header has # in front of first column name, fix it
    colnames(eggnog)[1] <- "query"
    colnames(eggnog)[colnames(eggnog) == "GOs"] <- "GO_terms"
    colnames(eggnog)[colnames(eggnog) == "Preferred_name"] <- "Preferred_name"
    
    cat("eggNOG rows:", nrow(eggnog), "\n")
    cat("eggNOG columns:\n")
    print(colnames(eggnog))

# Check key columns
    head(eggnog[, c("query", "Description", "Preferred_name", "GO_terms")], 5)

# InterProScan - 15 columns, tab-separated
    col_names_ipr <- c("protein", "md5", "length", "analysis", "signature",
                       "signature_desc", "start", "stop", "score", "status",
                       "date", "interpro_id", "interpro_desc", "go_terms", "pathways")
    
    interpro <- read.table("interproscan.tabular", sep = "\t", stringsAsFactors = FALSE,
                           quote = "", comment.char = "", fill = TRUE,
                           col.names = col_names_ipr)
    
    cat("\nInterProScan rows:", nrow(interpro), "\n")
    cat("InterProScan columns:", ncol(interpro), "\n")
    head(interpro[, c("protein", "analysis", "signature_desc", "go_terms")], 5)

# Strip the .p suffix from eggNOG and InterPro IDs to match
    eggnog$transcript_base <- gsub("\\.p\\d+$", "", eggnog$query)
    interpro$transcript_base <- gsub("\\.p\\d+$", "", interpro$protein)

# ============================================
# 2. BUILD MASTER ANNOTATION TABLE
# ============================================

# Best hit per transcript from Diamond nucleotide
    best_hits_nt <- diamond_nt %>%
      group_by(transcript) %>%
      slice_min(evalue, n = 1) %>%
      ungroup()

# Best hit per transcript from Diamond protein
    best_hits_prot <- diamond_prot %>%
      group_by(transcript) %>%
      slice_min(evalue, n = 1) %>%
      ungroup()

# Combine with eggNOG
    annotations <- data.frame(
      transcript = rownames(norm_counts),
      row.names = rownames(norm_counts)
    )

# Add Diamond nt hits
    annotations$uniprot_id <- best_hits_nt$uniprot_id[match(annotations$transcript, best_hits_nt$transcript)]
    annotations$description <- best_hits_nt$description[match(annotations$transcript, best_hits_nt$transcript)]
    annotations$evalue_nt <- best_hits_nt$evalue[match(annotations$transcript, best_hits_nt$transcript)]

# Add eggNOG GO terms
    eggnog_short <- eggnog[, c("query", "GO_terms", "KEGG_ko", "KEGG_Pathway", "COG_category", "Description")]
    annotations$GO_terms <- eggnog_short$GO_terms[match(annotations$transcript, eggnog_short$query)]
    annotations$KEGG_ko <- eggnog_short$KEGG_ko[match(annotations$transcript, eggnog_short$query)]
    annotations$KEGG_pathway <- eggnog_short$KEGG_Pathway[match(annotations$transcript, eggnog_short$query)]
    annotations$COG_category <- eggnog_short$COG_category[match(annotations$transcript, eggnog_short$query)]
    annotations$eggNOG_desc <- eggnog_short$Description[match(annotations$transcript, eggnog_short$query)]

# Save master annotation
    save(annotations, best_hits_nt, best_hits_prot, eggnog, interpro,
         file = "master_annotation.RData")

# ============================================
# 3. ANNOTATE KEY GENE SETS
# ============================================

# Load gene lists
    avic_core <- read.table("avicularium_core_genes.txt", stringsAsFactors = FALSE)[,1]
    rhiz_up <- read.table("rhizostol_up_genes.txt", stringsAsFactors = FALSE)[,1]
    shared_all <- read.table("shared_all_6_tissues.txt", stringsAsFactors = FALSE)[,1]

# Function to annotate a gene list
    annotate_genes <- function(gene_list) {
      data.frame(
        transcript = gene_list,
        description = annotations[gene_list, "description"],
        GO_terms = annotations[gene_list, "GO_terms"],
        KEGG_pathway = annotations[gene_list, "KEGG_pathway"],
        stringsAsFactors = FALSE
      )
    }
    
    avic_core_annotated <- annotate_genes(avic_core)
    rhiz_up_annotated <- annotate_genes(rhiz_up)
    shared_all_annotated <- annotate_genes(shared_all)

# Write annotated gene lists
    write.csv(avic_core_annotated, "avicularium_core_annotated.csv", row.names = FALSE)
    write.csv(rhiz_up_annotated, "rhizostol_up_annotated.csv", row.names = FALSE)
    write.csv(shared_all_annotated, "shared_all_annotated.csv", row.names = FALSE)

# ============================================
# 4. GO ENRICHMENT ANALYSIS
# ============================================

    # Prepare GO term mapping from eggNOG
    go_list <- strsplit(eggnog$GO_terms, ",")
    names(go_list) <- eggnog$query
    go_list <- go_list[!is.na(go_list)]
    
    # Unlist to create gene-to-GO mapping
    go_mapping <- data.frame(
      transcript = rep(names(go_list), sapply(go_list, length)),
      GO = unlist(go_list),
      stringsAsFactors = FALSE
    )
    go_mapping <- go_mapping[go_mapping$GO != "-" & !is.na(go_mapping$GO), ]

# GO enrichment function
    run_go_enrichment <- function(gene_set, name, universe = rownames(norm_counts)) {
      cat("\n=== GO Enrichment:", name, "===\n")
      
      ego <- enricher(
        gene = gene_set,
        universe = universe,
        TERM2GENE = go_mapping[, c("GO", "transcript")],
        pvalueCutoff = 0.05,
        qvalueCutoff = 0.1
      )
      
      if(!is.null(ego) && nrow(ego) > 0) {
        # Save results
        write.csv(as.data.frame(ego), paste0("GO_enrichment_", name, ".csv"))
    
# Dot plot
    if(nrow(ego) <= 30) {
      p <- dotplot(ego, showCategory = 20) + 
        ggtitle(paste("GO Enrichment:", name))
      ggsave(paste0("GO_dotplot_", name, ".png"), p, width = 10, height = 8)
    }
    
    cat("  Found", nrow(ego), "enriched GO terms\n")
    print(head(ego, 10))
    
    return(ego)
      } else {
        cat("  No significant enrichment found\n")
        return(NULL)
      }
    }
    
    # Run GO enrichment on key gene sets
    go_avic_core <- run_go_enrichment(avic_core, "Avicularium_core")
    go_rhiz_up <- run_go_enrichment(rhiz_up, "Rhizostol_up")
    go_shared <- run_go_enrichment(shared_all, "Shared_all_tissues")
    
    # GO enrichment on unique genes per tissue
    for(tissue in names(unique_genes)) {
      if(length(unique_genes[[tissue]]) > 10) {
        run_go_enrichment(unique_genes[[tissue]], paste0("Unique_", tissue))
      }
    }

# ============================================
# 5. COMPARE GO TERMS BETWEEN TISSUES
# ============================================

    # What GO terms are enriched in avicularium vs autozooid?
    cat("\n=== Comparing Avicularium vs Autozooid GO terms ===\n")
    if(!is.null(go_avic_core)) {
      cat("Top avicularium GO terms:\n")
      print(head(go_avic_core$Description, 10))
    }
    
    if(!is.null(go_rhiz_up)) {
      cat("\nTop rhizoid GO terms:\n")
      print(head(go_rhiz_up$Description, 10))
    }

# ============================================
# 6. IDENTIFY TRANSCRIPTION FACTORS & KEY GENES
# ============================================

    # From InterProScan, extract TF domains
    tf_domains <- c("Homeobox", "Zinc finger", "bHLH", "Forkhead", "HMG box",
                    "Nuclear hormone receptor", "Paired box", "T-box", "ETS")
    
    tf_genes <- interpro$protein[grep(paste(tf_domains, collapse = "|"), 
                                      interpro$signature_desc, ignore.case = TRUE)]
    tf_genes <- unique(tf_genes)
    cat("\n=== Transcription factors found:", length(tf_genes), "===\n")
    
    # TFs in avicularium core
    tf_avic <- intersect(tf_genes, avic_core)
    cat("TFs in avicularium core:", length(tf_avic), "\n")
    if(length(tf_avic) > 0) {
      tf_avic_annotated <- annotate_genes(tf_avic)
      write.csv(tf_avic_annotated, "TFs_avicularium_core.csv", row.names = FALSE)
    }
    
    # TFs in rhizostol
    tf_rhiz <- intersect(tf_genes, rhiz_up)
    cat("TFs in rhizostol up:", length(tf_rhiz), "\n")
    if(length(tf_rhiz) > 0) {
      tf_rhiz_annotated <- annotate_genes(tf_rhiz)
      write.csv(tf_rhiz_annotated, "TFs_rhizostol_up.csv", row.names = FALSE)
    }

# ============================================
# 7. ANNOTATE TOP DEGs FOR FIGURES
# ============================================

    # Annotate top 50 DEGs from each comparison
    for(name in names(degs_list)) {
      res <- degs_list[[name]]
      sig <- res[which(res$padj < 0.05), ]
      sig <- sig[order(sig$padj), ]
      top50 <- head(rownames(sig), 50)
      
      top50_df <- data.frame(
        transcript = top50,
        log2FC = sig[top50, "log2FoldChange"],
        padj = sig[top50, "padj"],
        description = annotations[top50, "description"],
        eggNOG_desc = annotations[top50, "eggNOG_desc"],
        stringsAsFactors = FALSE
      )
      
      write.csv(top50_df, paste0("Top50_DEGs_", name, "_annotated.csv"), row.names = FALSE)
    }

# ============================================
# 8. SAVE EVERYTHING
# ============================================

    save(annotations, go_avic_core, go_rhiz_up, go_shared,
         avic_core_annotated, rhiz_up_annotated, shared_all_annotated,
         tf_genes, tf_avic, tf_rhiz,
         file = "full_analysis_with_annotations.RData")
    
    cat("\n==================================\n")
    cat("Analysis complete!\n")
    cat("Ready to generate publication figures\n")
    cat("==================================\n")
    
    # ============================================
    # THE KEY OUTPUT: What are the annotated genes?
    # ============================================
    
    cat("\n=========================================\n")
    cat("AVICULARIUM CORE GENES (930 total)\n")
    cat("=========================================\n")
    
    # Show genes with real names (not just "uncharacterized")
    avic_with_names <- avic_core_annotated[!is.na(avic_core_annotated$description) & 
                                             avic_core_annotated$description != "-", ]
    cat("Genes with annotations:", nrow(avic_with_names), "/", nrow(avic_core_annotated), "\n\n")

# Top descriptions
    cat("=== Top descriptions in Avicularium Core ===\n")
    avic_desc_table <- sort(table(avic_with_names$description), decreasing = TRUE)
    print(head(avic_desc_table, 40))
    
    cat("\n=========================================\n")
    cat("RHIZOSTOL UPREGULATED GENES (1,972 total)\n")
    cat("=========================================\n")
    
    rhiz_with_names <- rhiz_up_annotated[!is.na(rhiz_up_annotated$description) & 
                                           rhiz_up_annotated$description != "-", ]
    cat("Genes with annotations:", nrow(rhiz_with_names), "/", nrow(rhiz_up_annotated), "\n\n")
    
    cat("=== Top descriptions in Rhizostol Up ===\n")
    rhiz_desc_table <- sort(table(rhiz_with_names$description), decreasing = TRUE)
    print(head(rhiz_desc_table, 40))
    
    cat("\n=========================================\n")
    cat("SHARED ALL TISSUES (347 genes)\n")
    cat("=========================================\n")
    
    shared_with_names <- shared_all_annotated[!is.na(shared_all_annotated$description) & 
                                                shared_all_annotated$description != "-", ]
    cat("Genes with annotations:", nrow(shared_with_names), "/", nrow(shared_all_annotated), "\n\n")
    
    cat("=== Top descriptions in Shared All ===\n")
    shared_desc_table <- sort(table(shared_with_names$description), decreasing = TRUE)
    print(head(shared_desc_table, 40))

# ============================================
# SEARCH FOR KEY TERMS IN AVICULARIUM
# ============================================
    
    cat("\n=========================================\n")
    cat("KEYWORD SEARCH IN AVICULARIUM CORE\n")
    cat("=========================================\n")

    keywords <- c("muscle", "actin", "myosin", "contraction", "movement",
                  "neur", "synap", "signal", "receptor", "channel",
                  "cuticle", "chitin", "collagen", "structural", "skeleton",
                  "defense", "toxin", "venom", "immun",
                  "develop", "differentiation", "morphogen",
                  "regeneration", "stem cell", "proliferation")
    
    for(kw in keywords) {
      hits <- grep(kw, avic_with_names$description, ignore.case = TRUE, value = TRUE)
      if(length(hits) > 0) {
        cat("\n--- '", kw, "' (", length(hits), " genes) ---\n", sep = "")
        print(head(unique(hits), 5))
      }
    }

# ============================================
# SEARCH FOR KEY TERMS IN RHIZOSTOL
# ============================================
    
    cat("\n=========================================\n")
    cat("KEYWORD SEARCH IN RHIZOSTOL UP\n")
    cat("=========================================\n")
    
    for(kw in keywords) {
      hits <- grep(kw, rhiz_with_names$description, ignore.case = TRUE, value = TRUE)
      if(length(hits) > 0) {
        cat("\n--- '", kw, "' (", length(hits), " genes) ---\n", sep = "")
        print(head(unique(hits), 5))
      }
    }
#################################################3


# Extract only Bugula neritina hits (most reliable)
    cat("\n=== BUGULA NERITINA HITS IN AVICULARIUM CORE ===\n")
    avic_bugula <- avic_with_names[grep("BUGNE", avic_with_names$description), ]
    avic_bugula$gene_name <- gsub(".*GN=(\\S+)\\s.*", "\\1", avic_bugula$description)
    avic_bugula$gene_name <- gsub(".*_(\\S+)\\sOS=.*", "\\1", avic_bugula$description)

# Get unique gene names
    avic_bugula_genes <- unique(avic_bugula$gene_name)
    cat("Unique Bugula neritina genes in avicularium core:", length(avic_bugula_genes), "\n")
    print(sort(avic_bugula_genes))
    
    cat("\n=== BUGULA NERITINA HITS IN RHIZOSTOL UP ===\n")
    rhiz_bugula <- rhiz_with_names[grep("BUGNE", rhiz_with_names$description), ]
    rhiz_bugula$gene_name <- gsub(".*GN=(\\S+)\\s.*", "\\1", rhiz_bugula$description)
    rhiz_bugula$gene_name <- gsub(".*_(\\S+)\\sOS=.*", "\\1", rhiz_bugula$description)
    
    rhiz_bugula_genes <- unique(rhiz_bugula$gene_name)
    cat("Unique Bugula neritina genes in rhizostol:", length(rhiz_bugula_genes), "\n")
    print(sort(rhiz_bugula_genes))

# Write these for your paper
    write.csv(avic_bugula, "avicularium_Bugula_neritina_hits.csv", row.names = FALSE)
    write.csv(rhiz_bugula, "rhizostol_Bugula_neritina_hits.csv", row.names = FALSE)

# Compare: what genes are in avicularium but NOT rhizoid?
    avic_unique_genes <- setdiff(avic_bugula_genes, rhiz_bugula_genes)
    rhiz_unique_genes <- setdiff(rhiz_bugula_genes, avic_bugula_genes)
    shared_bugula_genes <- intersect(avic_bugula_genes, rhiz_bugula_genes)
    
    cat("\nAvicularium-specific Bugula genes:", length(avic_unique_genes), "\n")
    print(avic_unique_genes)
    cat("\nRhizostol-specific Bugula genes:", length(rhiz_unique_genes), "\n")
    print(rhiz_unique_genes)
    cat("\nShared:", length(shared_bugula_genes), "\n")
    print(shared_bugula_genes)







# ============================================
# FIGURE 1: PCA - Global tissue relationships
# ============================================

    pca <- plotPCA(vsd, intgroup = "tissue", returnData = TRUE)
    percentVar <- round(100 * attr(pca, "percentVar"))
    
    # Add developmental stage
    pca$stage <- ifelse(grepl("Bud", pca$tissue), "Bud", "Mature")
    pca$stage[grep("Rhiz", pca$tissue)] <- "Rhizoid"
    
    # Custom colors
    tissue_cols <- c("AutoBud" = "#E41A1C", "AutoMat" = "#377EB8", 
                     "AvicBud" = "#4DAF4A", "AvicMat" = "#984EA3",
                     "RhizAuto" = "#FF7F00", "RhizStol" = "#A65628")
    
    p1 <- ggplot(pca, aes(PC1, PC2, color = tissue, shape = stage)) +
      geom_point(size = 5, alpha = 0.85) +
      geom_text_repel(aes(label = name), size = 3, show.legend = FALSE) +
      scale_color_manual(values = tissue_cols) +
      xlab(paste0("PC1: ", percentVar[1], "% variance")) +
      ylab(paste0("PC2: ", percentVar[2], "% variance")) +
      ggtitle("Bugulina stolonifera Zooid Transcriptomes") +
      theme_minimal(base_size = 14) +
      theme(legend.position = "bottom",
            plot.title = element_text(face = "bold", hjust = 0.5))
    
    ggsave("Figure1_PCA.png", p1, width = 10, height = 8, dpi = 300)
    print(p1)
<img width="1067" height="880" alt="image" src="https://github.com/user-attachments/assets/9a047ca0-f417-444c-9f4e-5ec62dccc318" />

# ============================================
# FIGURE 2: Sample distance heatmap
# ============================================

    sampleDists <- dist(t(assay(vsd)))
    sampleDistMatrix <- as.matrix(sampleDists)
    
    ann_col <- data.frame(Tissue = samples$tissue, 
                          Stage = ifelse(grepl("Bud", samples$tissue), "Bud",
                                         ifelse(grepl("Rhiz", samples$tissue), "Rhizoid", "Mature")))
    rownames(ann_col) <- colnames(sampleDistMatrix)
    
    ann_colors <- list(
      Tissue = tissue_cols,
      Stage = c("Bud" = "#FDB462", "Mature" = "#80B1D3", "Rhizoid" = "#B3DE69")
    )
    
    png("Figure2_SampleDistance.png", width = 8, height = 7, units = "in", res = 300)
    pheatmap(sampleDistMatrix,
             clustering_distance_rows = sampleDists,
             clustering_distance_cols = sampleDists,
             annotation_col = ann_col,
             annotation_colors = ann_colors,
             main = "Sample Distance Matrix",
             color = colorRampPalette(rev(brewer.pal(9, "Blues")))(100))
    dev.off()
<img width="1067" height="880" alt="image" src="https://github.com/user-attachments/assets/3126e7d3-72d7-4dd4-a1fc-9760eb52be91" />

# ============================================
# FIGURE 3: DEG counts barplot
# ============================================

    deg_summary <- data.frame(
      Comparison = names(deg_counts),
      DEGs = as.numeric(deg_counts),
      stringsAsFactors = FALSE
    )
    
    # Clean up names
    deg_summary$Comparison <- gsub("_vs_", " vs ", deg_summary$Comparison)
    deg_summary$Comparison <- factor(deg_summary$Comparison, 
                                     levels = deg_summary$Comparison[order(deg_summary$DEGs)])
    
    # Color by comparison type
    deg_summary$Type <- ifelse(grepl("Avic.*Auto", deg_summary$Comparison), "Avic vs Auto",
                               ifelse(grepl("Rhiz.*Auto", deg_summary$Comparison), "Rhiz vs Auto",
                                      ifelse(grepl("Rhiz.*Rhiz", deg_summary$Comparison), "Rhiz vs Rhiz",
                                             ifelse(grepl("Mat.*Bud", deg_summary$Comparison), "Mature vs Bud", "Other"))))
    
    p3 <- ggplot(deg_summary, aes(x = Comparison, y = DEGs, fill = Type)) +
      geom_bar(stat = "identity", width = 0.7) +
      geom_text(aes(label = DEGs), hjust = -0.2, size = 4) +
      coord_flip() +
      scale_fill_brewer(palette = "Set2") +
      labs(title = "Differentially Expressed Genes per Comparison",
           subtitle = paste0("Total expressed genes: ", nrow(norm_counts)),
           y = "Number of DEGs (padj < 0.05)", x = "") +
      theme_minimal(base_size = 13) +
      theme(legend.position = "bottom")
    
    ggsave("Figure3_DEG_counts.png", p3, width = 12, height = 6, dpi = 300)
    print(p3)
<img width="1067" height="880" alt="image" src="https://github.com/user-attachments/assets/148db39d-b201-4b76-91b8-6b15b62c8df3" />

# ============================================
# FIGURE 4: Volcano plot - AvicMat vs AutoMat
# ============================================

    res_avic_auto <- degs_list[["AvicMat_vs_AutoMat"]]
    res_df <- as.data.frame(res_avic_auto)
    res_df$gene <- rownames(res_df)
    res_df$sig <- "NS"
    res_df$sig[res_df$padj < 0.05 & res_df$log2FoldChange > 1] <- "Avic ↑"
    res_df$sig[res_df$padj < 0.05 & res_df$log2FoldChange < -1] <- "Auto ↑"
    res_df$sig[is.na(res_df$sig)] <- "NS"
    
    # Add Bugula neritina annotations for top genes
    res_df$label <- ""
    top_genes <- head(res_df[order(res_df$padj), ], 20)
    res_df$label[res_df$gene %in% top_genes$gene] <- annotations[top_genes$gene, "Preferred_name"]
    
    # Clean up labels
    res_df$label <- gsub("tr\\|.*\\|.*\\|(\\S+)\\s.*", "\\1", res_df$label)
    res_df$label[res_df$label == "-" | is.na(res_df$label)] <- ""
    
    p4 <- ggplot(res_df, aes(log2FoldChange, -log10(padj), color = sig)) +
      geom_point(size = 0.8, alpha = 0.6) +
      scale_color_manual(values = c("Avic ↑" = "#984EA3", "Auto ↑" = "#377EB8", "NS" = "grey80")) +
      geom_vline(xintercept = c(-1, 1), linetype = "dashed", alpha = 0.3) +
      geom_hline(yintercept = -log10(0.05), linetype = "dashed", alpha = 0.3) +
      geom_text_repel(aes(label = label), size = 2.5, max.overlaps = 15, color = "black") +
      labs(title = "Avicularium vs Autozooid (Mature)",
           subtitle = paste0(sum(res_df$sig == "Avic ↑"), " avicularium-up | ", 
                             sum(res_df$sig == "Auto ↑"), " autozooid-up"),
           x = "log2 Fold Change", y = "-log10 adjusted p-value") +
      theme_minimal(base_size = 13)
    
    ggsave("Figure4_Volcano_AvicMat_vs_AutoMat.png", p4, width = 10, height = 8, dpi = 300)
    print(p4)
<img width="1067" height="880" alt="image" src="https://github.com/user-attachments/assets/6ad2927d-8020-454c-bb43-3f3d69e0fe82" />

# ============================================
# FIGURE 5: Volcano plot - RhizStol vs AutoBud
# ============================================

    res_rhiz_auto <- degs_list[["RhizStol_vs_AutoBud"]]
    res_df2 <- as.data.frame(res_rhiz_auto)
    res_df2$gene <- rownames(res_df2)
    res_df2$sig <- "NS"
    res_df2$sig[res_df2$padj < 0.05 & res_df2$log2FoldChange > 1] <- "RhizStol ↑"
    res_df2$sig[res_df2$padj < 0.05 & res_df2$log2FoldChange < -1] <- "AutoBud ↑"
    res_df2$sig[is.na(res_df2$sig)] <- "NS"
    
    top_genes2 <- head(res_df2[order(res_df2$padj), ], 20)
    res_df2$label <- ""
    res_df2$label[res_df2$gene %in% top_genes2$gene] <- annotations[top_genes2$gene, "Preferred_name"]
    res_df2$label <- gsub("tr\\|.*\\|.*\\|(\\S+)\\s.*", "\\1", res_df2$label)
    res_df2$label[res_df2$label == "-" | is.na(res_df2$label)] <- ""
    
    p5 <- ggplot(res_df2, aes(log2FoldChange, -log10(padj), color = sig)) +
      geom_point(size = 0.8, alpha = 0.6) +
      scale_color_manual(values = c("RhizStol ↑" = "#A65628", "AutoBud ↑" = "#E41A1C", "NS" = "grey80")) +
      geom_vline(xintercept = c(-1, 1), linetype = "dashed", alpha = 0.3) +
      geom_hline(yintercept = -log10(0.05), linetype = "dashed", alpha = 0.3) +
      geom_text_repel(aes(label = label), size = 2.5, max.overlaps = 15, color = "black") +
      labs(title = "Rhizoid Network vs Autozooid Bud",
           subtitle = paste0(sum(res_df2$sig == "RhizStol ↑"), " rhizoid-up | ", 
                             sum(res_df2$sig == "AutoBud ↑"), " autozooid-up"),
           x = "log2 Fold Change", y = "-log10 adjusted p-value") +
      theme_minimal(base_size = 13)
    
    ggsave("Figure5_Volcano_RhizStol_vs_AutoBud.png", p5, width = 10, height = 8, dpi = 300)
    print(p5)
<img width="1067" height="880" alt="image" src="https://github.com/user-attachments/assets/e0b05615-18df-4d24-a0ea-db99a73babbf" />

# ============================================
# FIGURE 6: Tissue-specific genes heatmap
# ============================================

    # Get top 10 most specific genes per tissue (by tau)
    top_specific <- c()
    for(tissue in colnames(tissue_means)[1:6]) {
      tissue_genes <- rownames(tissue_means)[tissue_means[, tissue] > 10]
      tissue_tau <- tau[tissue_genes]
      top10 <- names(head(sort(tissue_tau, decreasing = TRUE), 10))
      top_specific <- c(top_specific, top10)
    }
    top_specific <- unique(top_specific)
    
    heatmap_data <- norm_counts[top_specific, ]
    rownames(heatmap_data) <- annotations[rownames(heatmap_data), "Preferred_name"]
    rownames(heatmap_data)[is.na(rownames(heatmap_data)) | rownames(heatmap_data) == "-"] <- 
      names(which(is.na(rownames(heatmap_data)) | rownames(heatmap_data) == "-"))
    
    png("Figure6_TissueSpecific_Heatmap.png", width = 12, height = 10, units = "in", res = 300)
    pheatmap(heatmap_data,
             annotation_col = data.frame(Tissue = samples$tissue, row.names = colnames(heatmap_data)),
             annotation_colors = list(Tissue = tissue_cols),
             scale = "row",
             show_rownames = TRUE,
             fontsize_row = 7,
             main = "Tissue-Specific Gene Expression",
             clustering_distance_cols = "correlation",
             color = colorRampPalette(rev(brewer.pal(11, "RdBu")))(100))
    dev.off()
<img width="1067" height="880" alt="image" src="https://github.com/user-attachments/assets/24f8b3b7-9d4a-4993-84c5-bf439d9805e3" />

# ============================================
# FIGURE 7: Shared vs Unique genes
# ============================================

    overlap_df <- data.frame(
      Tissue = colnames(expressed),
      Total = colSums(expressed),
      Unique = sapply(unique_genes, length),
      Shared = colSums(expressed) - sapply(unique_genes, length)
    )
    
    overlap_long <- pivot_longer(overlap_df, cols = c("Unique", "Shared"), 
                                 names_to = "Category", values_to = "Count")
    
    p7 <- ggplot(overlap_df, aes(x = reorder(Tissue, -Total), y = Total)) +
      geom_col(aes(fill = "Total"), width = 0.6, alpha = 0.3) +
      geom_col(aes(y = Shared, fill = "Shared"), width = 0.6) +
      geom_col(aes(y = Unique, fill = "Unique"), width = 0.6) +
      geom_text(aes(label = Unique, y = Unique/2), size = 5, fontface = "bold") +
      scale_fill_manual(values = c("Total" = "grey90", "Shared" = "#4DAF4A", "Unique" = "#E41A1C"),
                        labels = c("Shared with other tissues", "Total expressed", "Unique to this tissue")) +
      labs(title = "Genes Expressed per Zooid Type",
           subtitle = paste0("Unique = expressed only in that tissue | Total expressed genes: ", nrow(expressed)),
           y = "Number of genes", x = "") +
      theme_minimal(base_size = 13) +
      theme(legend.position = "bottom")
    
    ggsave("Figure7_Shared_vs_Unique.png", p7, width = 10, height = 6, dpi = 300)
    print(p7)
<img width="1067" height="880" alt="image" src="https://github.com/user-attachments/assets/7da311a1-d2a4-46b0-927d-a3f495aae730" />

# ============================================
# FIGURE 8: Jaccard similarity heatmap
# ============================================

    png("Figure8_Jaccard_Similarity.png", width = 7, height = 6, units = "in", res = 300)
    pheatmap(jaccard,
             display_numbers = TRUE,
             number_format = "%.2f",
             main = "Jaccard Similarity Between Zooid Types",
             color = colorRampPalette(c("white", "#2166AC"))(100),
             clustering_distance_rows = as.dist(1 - jaccard),
             clustering_distance_cols = as.dist(1 - jaccard))
    dev.off()
<img width="1067" height="880" alt="image" src="https://github.com/user-attachments/assets/947923a8-9e6d-4462-bc52-688113f4ff03" />

# ============================================
# SAVE ALL FIGURE DATA
# ============================================

    save(p1, p2, p3, p4, p5, p7, pca, deg_summary, res_df, res_df2,
         jaccard, overlap_df, top_specific,
         file = "figures_data.RData")
    
    cat("\n==================================\n")
    cat("All figures saved!\n")
    cat("==================================\n")
    cat("Figure 1: PCA\n")
    cat("Figure 2: Sample Distance Heatmap\n")
    cat("Figure 3: DEG Counts\n")
    cat("Figure 4: Volcano - Avicularium vs Autozooid (Mature)\n")
    cat("Figure 5: Volcano - Rhizoid vs Autozooid (Bud)\n")
    cat("Figure 6: Tissue-Specific Genes Heatmap\n")
    cat("Figure 7: Shared vs Unique Genes\n")
    cat("Figure 8: Jaccard Similarity\n")
    

# ============================================
# SINGLE VOLCANO PLOT - ALL COMPARISONS OVERLAID
# Each tissue type has its own color
# ============================================

    library(DESeq2)
    library(ggplot2)
    library(ggrepel)
    library(dplyr)
    
    # Load data
    load("bugulina_expression.RData")
    load("full_analysis_with_annotations.RData")
    
    # Tissue colors
    tissue_cols <- c(
      "AutoBud" = "#E41A1C",
      "AutoMat" = "#377EB8", 
      "AvicBud" = "#4DAF4A",
      "AvicMat" = "#984EA3",
      "RhizAuto" = "#FF7F00",
      "RhizStol" = "#A65628"
    )
    
    # Combine all DEG results into one dataframe
    all_degs <- data.frame()
    
    for(name in names(degs_list)) {
      res <- degs_list[[name]]
      parts <- strsplit(name, "_vs_")[[1]]
      tissue1 <- parts[1]
      tissue2 <- parts[2]
      
      # Get significant DEGs
      sig <- res[which(res$padj < 0.05 & abs(res$log2FoldChange) > 1), ]
      
      if(nrow(sig) > 0) {
        df <- data.frame(
          gene = rownames(sig),
          log2FC = sig$log2FoldChange,
          padj = sig$padj,
          comparison = name,
          # Color by which tissue is upregulated
          direction = ifelse(sig$log2FoldChange > 0, tissue1, tissue2),
          stringsAsFactors = FALSE
        )
        all_degs <- rbind(all_degs, df)
      }
    }
    
    cat("Total significant DEGs across all comparisons:", nrow(all_degs), "\n")
    cat("DEGs per tissue direction:\n")
    print(table(all_degs$direction))
    
    # Add gene names for the very top DEGs (most significant overall)
    all_degs <- all_degs[order(all_degs$padj), ]
    top_genes <- head(unique(all_degs$gene), 30)
    
    all_degs$label <- ""
    for(gene in top_genes) {
      gene_name <- annotations[gene, "Preferred_name"]
      if(!is.na(gene_name) && gene_name != "-") {
        gene_name <- gsub("tr\\|.*\\|.*\\|(\\S+)\\sOS=.*", "\\1", gene_name)
        all_degs$label[all_degs$gene == gene] <- gene_name
      }
    }

# Create the combined volcano plot
    p_combined <- ggplot(all_degs, aes(log2FC, -log10(padj))) +
      # Background: all points in grey
      geom_point(data = all_degs, aes(color = direction), size = 0.8, alpha = 0.5) +
      scale_color_manual(values = tissue_cols, name = "Upregulated in:") +
      # Threshold lines
      geom_vline(xintercept = c(-1, 1), linetype = "dashed", alpha = 0.3, color = "grey40") +
      geom_hline(yintercept = -log10(0.05), linetype = "dashed", alpha = 0.3, color = "grey40") +
      # Labels for top genes
      geom_text_repel(aes(label = label), size = 2.5, max.overlaps = 20, 
                      color = "black", box.padding = 0.3) +
      labs(title = "Differential Expression Across All Zooid Comparisons",
           subtitle = paste0("Total DEGs: ", nrow(all_degs), 
                             " | padj < 0.05, |log2FC| > 1"),
           x = "log2 Fold Change", 
           y = "-log10 adjusted p-value") +
      theme_minimal(base_size = 13) +
      theme(legend.position = "right",
            plot.title = element_text(face = "bold", size = 14),
            plot.subtitle = element_text(size = 10))
    
    ggsave("Volcano_All_Comparisons.png", p_combined, width = 12, height = 8, dpi = 300)
    print(p_combined)
<img width="1067" height="880" alt="image" src="https://github.com/user-attachments/assets/8e51286f-f82e-48d4-8b88-ac269de6aafc" />

# Summary stats
    cat("\n=== DEGs upregulated per tissue ===\n")
    deg_direction_counts <- table(all_degs$direction)
    for(tissue in names(tissue_cols)) {
      count <- deg_direction_counts[tissue]
      if(!is.na(count)) {
        cat(tissue, ":", count, "DEGs\n")
      }
    }
            AutoBud : 5548 DEGs
            AutoMat : 2251 DEGs
            AvicBud : 2604 DEGs
            AvicMat : 2901 DEGs
            RhizAuto : 1299 DEGs
            RhizStol : 2402 DEGs
# ============================================
# CROSS-SPECIES BRYOZOAN TRANSCRIPTOMICS
# Bugulina flabellata vs Bugulina stolonifera
# ============================================

library(DESeq2)
library(tximport)
library(clusterProfiler)
library(enrichplot)
library(ggplot2)
library(dplyr)
library(tidyr)
library(pheatmap)
library(seqinr)
library(ggrepel)

> # Working directory is B_kaewa (B. flabellata data)
> setwd("C:/Users/chois652/OneDrive - University of Otago/Desktop/PhD thesis/thesis paper/genetic/Bryozoa RNA/B_kaewa")
> # Path to B. stolonifera data
> stol_dir <- "C:/Users/chois652/OneDrive - University of Otago/Desktop/PhD thesis/thesis paper/genetic/Bryozoa RNA/bugulina stolonifera"
> # Load B. stolonifera data from its folder
> load(file.path(stol_dir, "bugulina_expression.RData"))
> load(file.path(stol_dir, "tissue_specificity_analysis.RData"))
> load(file.path(stol_dir, "full_analysis_with_annotations.RData"))
> cat("\n=== B. stolonifera data loaded ===\n")

=== B. stolonifera data loaded ===
> cat("  norm_counts:", nrow(norm_counts), "transcripts x", ncol(norm_counts), "samples\n")
  norm_counts: 62577 transcripts x 18 samples
> cat("  annotations:", nrow(annotations), "rows x", ncol(annotations), "cols\n")
  annotations: 62577 rows x 9 cols
> cat("  Annotation columns:", paste(colnames(annotations), collapse=", "), "\n")
  Annotation columns: transcript, uniprot_id, description, evalue_nt, GO_terms, KEGG_ko, KEGG_pathway, COG_category, eggNOG_desc 
> cat("\n=== Loading B. flabellata annotations ===\n")

=== Loading B. flabellata annotations ===
> # Diamond nucleotide
> flab_diamond_nt <- read.table("diamond_full_nt.txt", sep="\t", 
+                               stringsAsFactors=FALSE, quote="")
> colnames(flab_diamond_nt) <- c("transcript", "uniprot_id", "pident", "length",
+                                "mismatch", "gapopen", "qstart", "qend",
+                                "sstart", "send", "evalue", "bitscore", "description")
> # Diamond protein
> flab_diamond_prot <- read.table("diamond_full_prot.txt", sep="\t",
+                                 stringsAsFactors=FALSE, quote="")
> colnames(flab_diamond_prot) <- colnames(flab_diamond_nt)
> # eggNOG - NOTE: the file might be named differently; check both possibilities
> eggnog_file <- ifelse(file.exists("full_transcriptome_eggnog.emapper.annotations"),
+                       "full_transcriptome_eggnog.emapper.annotations",
+                       "eggnog.emapper.annotations")
> flab_eggnog <- read.table(eggnog_file,
+                           sep="\t", header=TRUE, stringsAsFactors=FALSE,
+                           quote="", comment.char="", na.strings="-",
+                           fill=TRUE, skip=4)
> colnames(flab_eggnog)[1] <- "query"
> colnames(flab_eggnog)[colnames(flab_eggnog)=="GOs"] <- "GO_terms"
> colnames(flab_eggnog)[colnames(flab_eggnog)=="Preferred_name"] <- "Preferred_name"
> # InterProScan
> col_names_ipr <- c("protein", "md5", "length", "analysis", "signature",
+                    "signature_desc", "start", "stop", "score", "status",
+                    "date", "interpro_id", "interpro_desc", "go_terms", "pathways")
> flab_interpro <- read.table("interproscan.tabular", sep="\t",
+                             stringsAsFactors=FALSE, quote="", comment.char="",
+                             fill=TRUE, col.names=col_names_ipr)
> # Load B. flabellata transcriptome sequences
> flab_fasta <- read.fasta("B_K_reference_transcriptome.fas")
> flab_transcripts <- names(flab_fasta)
> cat("B. flabellata transcripts:", length(flab_transcripts), "\n")
B. flabellata transcripts: 28142 
> # Strip .p suffixes for matching (eggNOG uses protein IDs like .p1, .p2)
> flab_eggnog$transcript_base <- gsub("\\.p\\d+$", "", flab_eggnog$query)
> flab_interpro$transcript_base <- gsub("\\.p\\d+$", "", flab_interpro$protein)
> cat("\n=== Building B. flabellata annotation table ===\n")

=== Building B. flabellata annotation table ===
> # Best hits per transcript from Diamond
> flab_best_nt <- flab_diamond_nt %>%
+   group_by(transcript) %>%
+   slice_min(evalue, n=1) %>%
+   slice_max(bitscore, n=1) %>%
+   ungroup()
> flab_best_prot <- flab_diamond_prot %>%
+   group_by(transcript) %>%
+   slice_min(evalue, n=1) %>%
+   slice_max(bitscore, n=1) %>%
+   ungroup()
> # Build annotation table with transcript IDs as rownames
> flab_annotations <- data.frame(
+   transcript = flab_transcripts,
+   row.names = flab_transcripts,
+   stringsAsFactors = FALSE
+ )
> # Diamond nt hits (match directly - transcript IDs should match)
> flab_annotations$uniprot_id <- flab_best_nt$uniprot_id[match(flab_annotations$transcript, flab_best_nt$transcript)]
> # Diamond nt hits (match directly - transcript IDs should match)
> flab_annotations$uniprot_id <- flab_best_nt$uniprot_id[match(flab_annotations$transcript, flab_best_nt$transcript)]
> flab_annotations$description <- flab_best_nt$description[match(flab_annotations$transcript, flab_best_nt$transcript)]
> flab_annotations$evalue_nt <- flab_best_nt$evalue[match(flab_annotations$transcript, flab_best_nt$transcript)]
> # eggNOG annotations - use transcript_base for matching (no .p suffix)
> flab_annotations$GO_terms <- flab_eggnog$GO_terms[match(flab_annotations$transcript, flab_eggnog$transcript_base)]
> flab_annotations$KEGG_ko <- flab_eggnog$KEGG_ko[match(flab_annotations$transcript, flab_eggnog$transcript_base)]
> flab_annotations$KEGG_pathway <- flab_eggnog$KEGG_Pathway[match(flab_annotations$transcript, flab_eggnog$transcript_base)]
> flab_annotations$COG_category <- flab_eggnog$COG_category[match(flab_annotations$transcript, flab_eggnog$transcript_base)]
> flab_annotations$eggNOG_desc <- flab_eggnog$Description[match(flab_annotations$transcript, flab_eggnog$transcript_base)]
> flab_annotations$Preferred_name <- flab_eggnog$Preferred_name[match(flab_annotations$transcript, flab_eggnog$transcript_base)]
> cat("B. flabellata annotations built:", nrow(flab_annotations), "transcripts\n")
B. flabellata annotations built: 28142 transcripts
> cat("  With Diamond BLAST hits:", sum(!is.na(flab_annotations$description)), "\n")
  With Diamond BLAST hits: 22830 
> cat("  With GO terms:", sum(!is.na(flab_annotations$GO_terms) & flab_annotations$GO_terms != "-"), "\n")
  With GO terms: 13689 
> cat("  With Preferred_name:", sum(!is.na(flab_annotations$Preferred_name) & flab_annotations$Preferred_name != "-"), "\n")
  With Preferred_name: 14030 
> cat("\n=== Verifying B. stolonifera annotations ===\n")

=== Verifying B. stolonifera annotations ===
> cat("  Rows:", nrow(annotations), "\n")
  Rows: 62577 
> cat("  With BLAST hits:", sum(!is.na(annotations$description)), "\n")
  With BLAST hits: 42256 
> # Check what GO column exists
> go_col_stol <- grep("GO", colnames(annotations), value=TRUE)
> cat("  GO columns found:", paste(go_col_stol, collapse=", "), "\n")
  GO columns found: GO_terms 
> if(length(go_col_stol) > 0) {
+   cat("  With GO terms:", sum(!is.na(annotations[[go_col_stol[1]]]) & annotations[[go_col_stol[1]]] != "-"), "\n")
+ }
  With GO terms: 0 
> # Check what the eggnog query IDs look like
> cat("Sample eggnog query IDs:\n")
Sample eggnog query IDs:
> print(head(eggnog$query, 5))
[1] "TRINITY_DN100005_c0_g2_i1.p2" "TRINITY_DN100014_c0_g1_i1.p1" "TRINITY_DN100038_c0_g1_i1.p1" "TRINITY_DN100054_c0_g1_i1.p1" "TRINITY_DN100065_c0_g1_i1.p1"
> cat("\nSample annotation transcript IDs:\n")

Sample annotation transcript IDs:
> print(head(annotations$transcript, 5))
[1] "TRINITY_DN174602_c0_g1_i1" "TRINITY_DN117250_c0_g2_i1" "TRINITY_DN117224_c0_g1_i1" "TRINITY_DN117257_c0_g1_i1" "TRINITY_DN117257_c0_g2_i1"
> # eggnog$transcript_base already exists (created in original script)
> # Let's verify
> if(!"transcript_base" %in% colnames(eggnog)) {
+   eggnog$transcript_base <- gsub("\\.p\\d+$", "", eggnog$query)
+ }
> # Now fix the GO terms using transcript_base for matching
> annotations$GO_terms <- eggnog$GO_terms[match(annotations$transcript, eggnog$transcript_base)]
> annotations$KEGG_ko <- eggnog$KEGG_ko[match(annotations$transcript, eggnog$transcript_base)]
> annotations$KEGG_pathway <- eggnog$KEGG_Pathway[match(annotations$transcript, eggnog$transcript_base)]
> annotations$COG_category <- eggnog$COG_category[match(annotations$transcript, eggnog$transcript_base)]
> annotations$eggNOG_desc <- eggnog$Description[match(annotations$transcript, eggnog$transcript_base)]
> # Also add Preferred_name if it exists
> if("Preferred_name" %in% colnames(eggnog)) {
+   annotations$Preferred_name <- eggnog$Preferred_name[match(annotations$transcript, eggnog$transcript_base)]
+ }
> # Verify the fix
> cat("\n=== After fix ===\n")

=== After fix ===
> cat("  With GO terms:", sum(!is.na(annotations$GO_terms) & annotations$GO_terms != "-" & annotations$GO_terms != ""), "\n")
  With GO terms: 20490 
> cat("  With Preferred_name:", sum(!is.na(annotations$Preferred_name) & annotations$Preferred_name != "-"), "\n")
  With Preferred_name: 20879 
> # Check a few examples
> cat("\nSample GO terms after fix:\n")

Sample GO terms after fix:
> go_fixed <- annotations$GO_terms[!is.na(annotations$GO_terms) & annotations$GO_terms != "-" & annotations$GO_terms != ""]
> print(head(go_fixed, 3))
[1] "GO:0000902,GO:0000904,GO:0002376,GO:0002520,GO:0003674,GO:0003824,GO:0004175,GO:0004197,GO:0005488,GO:0005515,GO:0005575,GO:0005622,GO:0005623,GO:0005634,GO:0005737,GO:0005739,GO:0005829,GO:0006508,GO:0006807,GO:0006915,GO:0006919,GO:0006950,GO:0006974,GO:0007154,GO:0007165,GO:0007166,GO:0007275,GO:0008047,GO:0008150,GO:0008152,GO:0008219,GO:0008233,GO:0008234,GO:0008630,GO:0008635,GO:0009314,GO:0009410,GO:0009411,GO:0009416,GO:0009628,GO:0009653,GO:0009719,GO:0009725,GO:0009893,GO:0009987,GO:0010033,GO:0010604,GO:0010941,GO:0010942,GO:0010950,GO:0010952,GO:0012501,GO:0014070,GO:0016043,GO:0016787,GO:0017124,GO:0019222,GO:0019538,GO:0019899,GO:0019900,GO:0019901,GO:0019904,GO:0023052,GO:0030097,GO:0030099,GO:0030154,GO:0030162,GO:0030220,GO:0030234,GO:0031323,GO:0031325,GO:0031960,GO:0032268,GO:0032270,GO:0032501,GO:0032502,GO:0032870,GO:0032989,GO:0032991,GO:0033554,GO:0033993,GO:0034644,GO:0034976,GO:0035556,GO:0035690,GO:0036344,GO:0038034,GO:0042221,GO:0042493,GO:0042770,GO:0042802,GO:0042981,GO:0043065,GO:0043067,GO:0043068,GO:0043085,GO:0043170,GO:0043226,GO:0043227,GO:0043229,GO:0043231,GO:0043280,GO:0043281,GO:0043293,GO:0043523,GO:0043525,GO:0044093,GO:0044238,GO:0044424,GO:0044444,GO:0044445,GO:0044464,GO:0045862,GO:0048468,GO:0048513,GO:0048518,GO:0048522,GO:0048534,GO:0048545,GO:0048583,GO:0048646,GO:0048731,GO:0048856,GO:0048869,GO:0050789,GO:0050790,GO:0050794,GO:0050896,GO:0051171,GO:0051173,GO:0051246,GO:0051247,GO:0051336,GO:0051345,GO:0051384,GO:0051716,GO:0052547,GO:0052548,GO:0060255,GO:0065007,GO:0065009,GO:0070011,GO:0070059,GO:0070887,GO:0071214,GO:0071310,GO:0071383,GO:0071384,GO:0071385,GO:0071396,GO:0071407,GO:0071466,GO:0071478,GO:0071482,GO:0071495,GO:0071548,GO:0071549,GO:0071704,GO:0071840,GO:0080090,GO:0080134,GO:0080135,GO:0097153,GO:0097190,GO:0097191,GO:0097192,GO:0097193,GO:0097194,GO:0097200,GO:0097327,GO:0098772,GO:0104004,GO:0140096,GO:1901214,GO:1901216,GO:1901564,GO:1901654,GO:1901655,GO:1901700,GO:1901701,GO:2000116,GO:2 ... <truncated>
[2] "GO:0000012,GO:0000302,GO:0000375,GO:0000377,GO:0000398,GO:0000785,GO:0003674,GO:0003676,GO:0003677,GO:0003682,GO:0003684,GO:0003690,GO:0003723,GO:0003725,GO:0003824,GO:0004518,GO:0004527,GO:0004529,GO:0004536,GO:0005488,GO:0005515,GO:0005575,GO:0005622,GO:0005623,GO:0005634,GO:0005654,GO:0005694,GO:0005730,GO:0006139,GO:0006259,GO:0006266,GO:0006281,GO:0006302,GO:0006396,GO:0006397,GO:0006725,GO:0006793,GO:0006796,GO:0006807,GO:0006950,GO:0006974,GO:0006979,GO:0008150,GO:0008152,GO:0008380,GO:0008409,GO:0008967,GO:0009636,GO:0009987,GO:0010035,GO:0010467,GO:0016070,GO:0016071,GO:0016311,GO:0016787,GO:0016788,GO:0016791,GO:0016796,GO:0016895,GO:0031647,GO:0031974,GO:0031981,GO:0033554,GO:0033699,GO:0034641,GO:0035312,GO:0042221,GO:0042493,GO:0042542,GO:0042578,GO:0043167,GO:0043169,GO:0043170,GO:0043226,GO:0043227,GO:0043228,GO:0043229,GO:0043231,GO:0043232,GO:0043233,GO:0044237,GO:0044238,GO:0044260,GO:0044422,GO:0044424,GO:0044427,GO:0044428,GO:0044446,GO:0044464,GO:0046403,GO:0046483,GO:0046677,GO:0046872,GO:0047485,GO:0050896,GO:0051219,GO:0051716,GO:0065007,GO:0065008,GO:0070013,GO:0071704,GO:0090304,GO:0090305,GO:0097159,GO:0098501,GO:0098506,GO:0098518,GO:0140097,GO:1901360,GO:1901363,GO:1901700"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       ... <truncated>
[3] "GO:0000902,GO:0000904,GO:0001085,GO:0001103,GO:0001654,GO:0001655,GO:0001736,GO:0001738,GO:0001754,GO:0002009,GO:0003008,GO:0003407,GO:0003674,GO:0005488,GO:0005515,GO:0005575,GO:0005622,GO:0005623,GO:0005737,GO:0005813,GO:0005815,GO:0005829,GO:0005856,GO:0005929,GO:0006810,GO:0006928,GO:0006935,GO:0006996,GO:0007017,GO:0007018,GO:0007164,GO:0007275,GO:0007389,GO:0007399,GO:0007409,GO:0007411,GO:0007417,GO:0007420,GO:0007423,GO:0007600,GO:0007606,GO:0007608,GO:0007610,GO:0007611,GO:0007612,GO:0007635,GO:0008104,GO:0008134,GO:0008150,GO:0008306,GO:0008355,GO:0009605,GO:0009653,GO:0009798,GO:0009887,GO:0009888,GO:0009987,GO:0010638,GO:0010970,GO:0015630,GO:0016020,GO:0016043,GO:0021537,GO:0021772,GO:0021988,GO:0022008,GO:0022607,GO:0030030,GO:0030031,GO:0030154,GO:0030182,GO:0030425,GO:0030705,GO:0030855,GO:0030900,GO:0031175,GO:0031344,GO:0031346,GO:0031503,GO:0032231,GO:0032386,GO:0032388,GO:0032391,GO:0032501,GO:0032502,GO:0032879,GO:0032880,GO:0032886,GO:0032956,GO:0032970,GO:0032989,GO:0032990,GO:0032991,GO:0033036,GO:0033043,GO:0034260,GO:0034464,GO:0034613,GO:0035264,GO:0035295,GO:0035869,GO:0036064,GO:0036477,GO:0040007,GO:0040011,GO:0042048,GO:0042073,GO:0042221,GO:0042330,GO:0042490,GO:0042995,GO:0043005,GO:0043010,GO:0043086,GO:0043087,GO:0043226,GO:0043228,GO:0043229,GO:0043232,GO:0043583,GO:0044085,GO:0044087,GO:0044092,GO:0044292,GO:0044422,GO:0044424,GO:0044430,GO:0044441,GO:0044444,GO:0044446,GO:0044463,GO:0044464,GO:0044782,GO:0045444,GO:0046530,GO:0046907,GO:0048468,GO:0048513,GO:0048518,GO:0048519,GO:0048522,GO:0048560,GO:0048589,GO:0048592,GO:0048593,GO:0048666,GO:0048667,GO:0048699,GO:0048729,GO:0048731,GO:0048812,GO:0048839,GO:0048856,GO:0048858,GO:0048869,GO:0050789,GO:0050790,GO:0050794,GO:0050877,GO:0050890,GO:0050893,GO:0050896,GO:0051049,GO:0051050,GO:0051128,GO:0051130,GO:0051179,GO:0051234,GO:0051270,GO:0051272,GO:0051336,GO:0051346,GO:0051492,GO:0051493,GO:0051641,GO:0051649,GO:0060041,GO:0060042,GO:0060113,GO:0060119,GO:0060122,GO:0 ... <truncated>
> # Save the fixed annotations
> save(annotations, eggnog, interpro, best_hits_nt, best_hits_prot,
+      file=file.path(stol_dir, "master_annotation.RData"))
> cat("\n=== B. stolonifera annotations FIXED ===\n")

=== B. stolonifera annotations FIXED ===
> cat("  With GO terms:", sum(!is.na(annotations$GO_terms) & annotations$GO_terms != "-"), "\n")
  With GO terms: 20490 
> cat("  With Preferred_name:", sum(!is.na(annotations$Preferred_name) & annotations$Preferred_name != "-"), "\n")
  With Preferred_name: 20879 
> cat("\n=== Identifying orthologs ===\n")

=== Identifying orthologs ===
> parse_blast <- function(file) {
+   df <- read.table(file, sep="\t", stringsAsFactors=FALSE)
+   colnames(df) <- c("qseqid", "sseqid", "pident", "length", "mismatch", 
+                     "gapopen", "qstart", "qend", "sstart", "send", "evalue", "bitscore")
+   return(df)
+ }
> flab_to_stol <- parse_blast("flab_to_stol.tab")
> stol_to_flab <- parse_blast("stol_to_flab.tab")
> cat("BLAST hits: B. flabellata -> B. stolonifera:", nrow(flab_to_stol), "\n")
BLAST hits: B. flabellata -> B. stolonifera: 63053 
> cat("BLAST hits: B. stolonifera -> B. flabellata:", nrow(stol_to_flab), "\n")
BLAST hits: B. stolonifera -> B. flabellata: 100558 
> best_flab_to_stol <- flab_to_stol %>%
+   group_by(qseqid) %>%
+   slice_min(evalue, n=1) %>%
+   slice_max(bitscore, n=1) %>%
+   ungroup()
> best_stol_to_flab <- stol_to_flab %>%
+   group_by(qseqid) %>%
+   slice_min(evalue, n=1) %>%
+   slice_max(bitscore, n=1) %>%
+   ungroup()
> orthologs <- best_flab_to_stol %>%
+   inner_join(best_stol_to_flab,
+              by=c("qseqid"="sseqid", "sseqid"="qseqid"),
+              suffix=c("_f2s", "_s2f"),
+              relationship = "many-to-many") %>%
+   rename(flab_transcript = qseqid,
+          stol_transcript = sseqid)
> cat("\n=== RECIPROCAL BEST HITS:", nrow(orthologs), "===\n")

=== RECIPROCAL BEST HITS: 15816 ===
> cat("B. flabellata transcripts with orthologs:", 
+     length(unique(orthologs$flab_transcript)), "/", length(flab_transcripts),
+     "(", round(100*length(unique(orthologs$flab_transcript))/length(flab_transcripts), 1), "%)\n")
B. flabellata transcripts with orthologs: 12683 / 28142 ( 45.1 %)
> cat("B. stolonifera transcripts with orthologs:",
+     length(unique(orthologs$stol_transcript)), "/", nrow(annotations),
+     "(", round(100*length(unique(orthologs$stol_transcript))/nrow(annotations), 1), "%)\n")
B. stolonifera transcripts with orthologs: 13187 / 62577 ( 21.1 %)
> cat("\n=== Building combined ortholog table ===\n")

=== Building combined ortholog table ===
> ortholog_table <- data.frame(
+   flab_transcript = orthologs$flab_transcript,
+   stol_transcript = orthologs$stol_transcript,
+   pident = orthologs$pident_f2s,
+   evalue = orthologs$evalue_f2s,
+   bitscore = orthologs$bitscore_f2s,
+   stringsAsFactors = FALSE
+ )
> # Add flabellata annotations
> ortholog_table$flab_desc <- flab_annotations[ortholog_table$flab_transcript, "description"]
> ortholog_table$flab_GO <- flab_annotations[ortholog_table$flab_transcript, "GO_terms"]
> ortholog_table$flab_eggNOG <- flab_annotations[ortholog_table$flab_transcript, "eggNOG_desc"]
> ortholog_table$flab_name <- flab_annotations[ortholog_table$flab_transcript, "Preferred_name"]
> # Add stolonifera annotations
> ortholog_table$stol_desc <- annotations[ortholog_table$stol_transcript, "description"]
> ortholog_table$stol_GO <- annotations[ortholog_table$stol_transcript, "GO_terms"]
> ortholog_table$stol_eggNOG <- annotations[ortholog_table$stol_transcript, "eggNOG_desc"]
> ortholog_table$stol_name <- annotations[ortholog_table$stol_transcript, "Preferred_name"]
> ortholog_table$same_desc <- ortholog_table$flab_desc == ortholog_table$stol_desc
> cat("Orthologs with identical BLAST descriptions:", 
+     sum(ortholog_table$same_desc, na.rm=TRUE), "/", nrow(ortholog_table),
+     "(", round(100*sum(ortholog_table$same_desc, na.rm=TRUE)/nrow(ortholog_table), 1), "%)\n")
Orthologs with identical BLAST descriptions: 12054 / 15816 ( 76.2 %)
> save(ortholog_table, orthologs, file="cross_species_orthologs.RData")
> write.csv(ortholog_table, "ortholog_table_annotated.csv", row.names=FALSE)
> cat("\n=== Mapping gene sets across species ===\n")

=== Mapping gene sets across species ===
> # Load B. stolonifera gene sets
> avic_core <- read.table(file.path(stol_dir, "avicularium_core_genes.txt"), 
+                         stringsAsFactors=FALSE)[,1]
> rhiz_up <- read.table(file.path(stol_dir, "rhizostol_up_genes.txt"), 
+                       stringsAsFactors=FALSE)[,1]
> shared_all <- read.table(file.path(stol_dir, "shared_all_6_tissues.txt"), 
+                          stringsAsFactors=FALSE)[,1]
> unique_genes_files <- list.files(stol_dir, pattern="^unique_.*\\.txt$", full.names=TRUE)
> unique_genes_stol <- list()
> for(f in unique_genes_files) {
+   tissue <- gsub("unique_(.*)\\.txt", "\\1", basename(f))
+   unique_genes_stol[[tissue]] <- read.table(f, stringsAsFactors=FALSE)[,1]
+ }
> map_to_flab <- function(stol_genes, ortholog_df) {
+   ortholog_df %>%
+     filter(stol_transcript %in% stol_genes) %>%
+     pull(flab_transcript) %>%
+     unique()
+ }
> avic_core_flab <- map_to_flab(avic_core, ortholog_table)
> rhiz_up_flab <- map_to_flab(rhiz_up, ortholog_table)
> shared_all_flab <- map_to_flab(shared_all, ortholog_table)
> unique_genes_flab <- list()
> for(tissue in names(unique_genes_stol)) {
+   unique_genes_flab[[tissue]] <- map_to_flab(unique_genes_stol[[tissue]], ortholog_table)
+ }
> cat("\n=========================================\n")

=========================================
> cat("GENE SET CONSERVATION SUMMARY\n")
GENE SET CONSERVATION SUMMARY
> cat("=========================================\n")
=========================================
> cat(sprintf("%-40s %5s/%-5s (%5.1f%%)\n", 
+             "Avicularium core genes:", 
+             length(avic_core_flab), length(avic_core),
+             100*length(avic_core_flab)/length(avic_core)))
Avicularium core genes:                    103/930   ( 11.1%)
> cat(sprintf("%-40s %5s/%-5s (%5.1f%%)\n", 
+             "Rhizostol-up genes:", 
+             length(rhiz_up_flab), length(rhiz_up),
+             100*length(rhiz_up_flab)/length(rhiz_up)))
Rhizostol-up genes:                        457/1972  ( 23.2%)
> cat(sprintf("%-40s %5s/%-5s (%5.1f%%)\n", 
+             "Shared all tissues:", 
+             length(shared_all_flab), length(shared_all),
+             100*length(shared_all_flab)/length(shared_all)))
Shared all tissues:                        301/347   ( 86.7%)
> for(tissue in names(unique_genes_flab)) {
+   n_stol <- length(unique_genes_stol[[tissue]])
+   n_flab <- length(unique_genes_flab[[tissue]])
+   if(n_stol > 0) {
+     cat(sprintf("  Unique %-15s %5d/%-5d (%5.1f%%)\n", 
+                 paste0(tissue, ":"), n_flab, n_stol,
+                 100*n_flab/n_stol))
+   }
+ }
  Unique AutoBud:           27/44    ( 61.4%)
  Unique AutoMat:           99/220   ( 45.0%)
  Unique AvicBud:           51/143   ( 35.7%)
  Unique AvicMat:           43/80    ( 53.8%)
  Unique RhizAuto:           8/16    ( 50.0%)
  Unique RhizStol:         107/266   ( 40.2%)
> # Save mapped gene sets
> write.table(avic_core_flab, "flabellata_avicularium_core_orthologs.txt", 
+             quote=FALSE, row.names=FALSE, col.names=FALSE)
> write.table(rhiz_up_flab, "flabellata_rhizostol_up_orthologs.txt",
+             quote=FALSE, row.names=FALSE, col.names=FALSE)
> write.table(shared_all_flab, "flabellata_shared_all_orthologs.txt",
+             quote=FALSE, row.names=FALSE, col.names=FALSE)
> cat("\n=== GO Enrichment Analysis ===\n")

=== GO Enrichment Analysis ===
> # GO mapping for B. flabellata
> flab_go_list <- strsplit(flab_eggnog$GO_terms, ",")
> names(flab_go_list) <- flab_eggnog$transcript_base
> flab_go_list <- flab_go_list[!is.na(flab_go_list)]
> flab_go_mapping <- data.frame(
+   transcript = rep(names(flab_go_list), sapply(flab_go_list, length)),
+   GO = unlist(flab_go_list),
+   stringsAsFactors = FALSE
+ )
> flab_go_mapping <- flab_go_mapping[!is.na(flab_go_mapping$GO) & 
+                                      flab_go_mapping$GO != "-" & 
+                                      flab_go_mapping$GO != "", ]
> # GO mapping for B. stolonifera
> stol_go_list <- strsplit(eggnog$GO_terms, ",")
> names(stol_go_list) <- eggnog$transcript_base
> stol_go_list <- stol_go_list[!is.na(stol_go_list)]
> stol_go_mapping <- data.frame(
+   transcript = rep(names(stol_go_list), sapply(stol_go_list, length)),
+   GO = unlist(stol_go_list),
+   stringsAsFactors = FALSE
+ )
> stol_go_mapping <- stol_go_mapping[!is.na(stol_go_mapping$GO) & 
+                                      stol_go_mapping$GO != "-" & 
+                                      stol_go_mapping$GO != "", ]
> cat("B. flabellata GO pairs:", nrow(flab_go_mapping), "\n")
B. flabellata GO pairs: 2244558 
> cat("B. stolonifera GO pairs:", nrow(stol_go_mapping), "\n")
B. stolonifera GO pairs: 4930374 
> run_go <- function(gene_set, name, go_map, universe) {
+   cat("\n--- GO:", name, "---\n")
+   if(length(gene_set) < 5) {
+     cat("  Too few genes\n")
+     return(NULL)
+   }
+   ego <- enricher(gene=gene_set, universe=universe,
+                   TERM2GENE=go_map[, c("GO", "transcript")],
+                   pvalueCutoff=0.05, qvalueCutoff=0.1)
+   if(!is.null(ego) && nrow(ego@result) > 0) {
+     cat("  Found", nrow(ego@result), "enriched terms\n")
+     write.csv(as.data.frame(ego), paste0("GO_", name, ".csv"))
+     return(ego)
+   } else {
+     cat("  No enrichment\n")
+     return(NULL)
+   }
+ }
> go_stol_avic <- run_go(avic_core, "Stol_Avicularium_core", stol_go_mapping, rownames(annotations))

--- GO: Stol_Avicularium_core ---
  Found 10862 enriched terms
> go_stol_rhiz <- run_go(rhiz_up, "Stol_Rhizostol_up", stol_go_mapping, rownames(annotations))

--- GO: Stol_Rhizostol_up ---
  Found 10862 enriched terms
> go_flab_avic <- run_go(avic_core_flab, "Flab_Avicularium_core", flab_go_mapping, flab_transcripts)

--- GO: Flab_Avicularium_core ---
  Found 9264 enriched terms
> go_flab_rhiz <- run_go(rhiz_up_flab, "Flab_Rhizostol_up", flab_go_mapping, flab_transcripts)

--- GO: Flab_Rhizostol_up ---
  Found 9264 enriched terms
> # Compare GO between species
> compare_go <- function(go_stol, go_flab, label) {
+   cat("\n=== GO Comparison:", label, "===\n")
+   if(is.null(go_stol) || is.null(go_flab)) {
+     cat("  Cannot compare\n")
+     return(NULL)
+   }
+   shared <- intersect(go_stol@result$ID, go_flab@result$ID)
+   cat("  Shared:", length(shared), "\n")
+   cat("  Stol only:", length(setdiff(go_stol@result$ID, go_flab@result$ID)), "\n")
+   cat("  Flab only:", length(setdiff(go_flab@result$ID, go_stol@result$ID)), "\n")
+   if(length(shared) > 0) {
+     cat("  Top shared:\n")
+     for(d in head(go_stol@result$Description[go_stol@result$ID %in% shared], 10)) {
+       cat("    -", d, "\n")
+     }
+   }
+   return(list(shared=shared))
+ }
> go_comp_avic <- compare_go(go_stol_avic, go_flab_avic, "Avicularium")

=== GO Comparison: Avicularium ===
  Shared: 8791 
  Stol only: 2071 
  Flab only: 473 
  Top shared:
    - GO:0030018 
    - GO:0031674 
    - GO:0035158 
    - GO:0043296 
    - GO:0097531 
    - GO:0001779 
    - GO:0035172 
    - GO:0030720 
    - GO:0042129 
    - GO:0001553 
> go_comp_rhiz <- compare_go(go_stol_rhiz, go_flab_rhiz, "Rhizostol")

=== GO Comparison: Rhizostol ===
  Shared: 8791 
  Stol only: 2071 
  Flab only: 473 
  Top shared:
    - GO:0098858 
    - GO:0030175 
    - GO:0004879 
    - GO:0098531 
    - GO:0005902 
    - GO:0030695 
    - GO:0005096 
    - GO:0050891 
    - GO:0046578 
    - GO:0030104 
> cat("\n=== Sequence Conservation ===\n")

=== Sequence Conservation ===
> analyze_cons <- function(stol_genes, flab_genes, name) {
+   pairs <- ortholog_table %>%
+     filter(stol_transcript %in% stol_genes & flab_transcript %in% flab_genes)
+   cat("\n---", name, "---\n")
+   cat("  Pairs:", nrow(pairs), "\n")
+   if(nrow(pairs) > 0) {
+     cat("  Mean identity:", round(mean(pairs$pident, na.rm=TRUE), 1), "%\n")
+     cat("  Median identity:", round(median(pairs$pident, na.rm=TRUE), 1), "%\n")
+     pairs$category <- name
+   }
+   return(pairs)
+ }
> avic_cons <- analyze_cons(avic_core, avic_core_flab, "Avicularium Core")

--- Avicularium Core ---
  Pairs: 103 
  Mean identity: 83.9 %
  Median identity: 84.5 %
> rhiz_cons <- analyze_cons(rhiz_up, rhiz_up_flab, "Rhizostol Up")

--- Rhizostol Up ---
  Pairs: 459 
  Mean identity: 84.1 %
  Median identity: 84.4 %
> shared_cons <- analyze_cons(shared_all, shared_all_flab, "Shared All")

--- Shared All ---
  Pairs: 303 
  Mean identity: 86.9 %
  Median identity: 86.9 %
> all_cons <- bind_rows(avic_cons, rhiz_cons, shared_cons)
> if(nrow(all_cons) > 0 && length(unique(all_cons$category)) > 1) {
+   kw <- kruskal.test(pident ~ category, data=all_cons)
+   cat("\nKruskal-Wallis p-value:", round(kw$p.value, 4), "\n")
+ }

Kruskal-Wallis p-value: 0 
> cat("\n=== Generating figures ===\n")

=== Generating figures ===
> # Conservation barplot
> cons_df <- data.frame(
+   GeneSet = c("Avicularium Core", "Rhizostol Up", "Shared All",
+               paste("Unique", names(unique_genes_stol))),
+   Stol = c(length(avic_core), length(rhiz_up), length(shared_all),
+            sapply(unique_genes_stol, length)),
+   Flab = c(length(avic_core_flab), length(rhiz_up_flab), length(shared_all_flab),
+            sapply(names(unique_genes_stol), function(t) length(unique_genes_flab[[t]])))
+ )
> cons_df$Pct <- 100 * cons_df$Flab / cons_df$Stol
> cons_df$GeneSet <- reorder(cons_df$GeneSet, cons_df$Pct)
> p1 <- ggplot(cons_df, aes(x=GeneSet, y=Pct)) +
+   geom_bar(stat="identity", fill="steelblue", width=0.7) +
+   geom_text(aes(label=paste0(Flab, "/", Stol)), hjust=-0.1, size=3.5) +
+   coord_flip(ylim=c(0, max(cons_df$Pct)*1.3)) +
+   labs(title="Gene Set Conservation Between Bugulina Species",
+        subtitle="B. flabellata orthologs as % of B. stolonifera gene sets",
+        y="% Conserved", x="") +
+   theme_minimal(base_size=13)
> ggsave("Figure_CrossSpecies_Conservation.png", p1, width=10, height=6, dpi=300)
> print(p1)
<img width="1066" height="878" alt="image" src="https://github.com/user-attachments/assets/68b5fc68-43a3-4096-978c-51c93b0b1899" />

> # Sequence identity plot
> if(nrow(all_cons) > 0) {
+   p2 <- ggplot(all_cons, aes(x=category, y=pident, fill=category)) +
+     geom_violin(alpha=0.5, draw_quantiles=0.5) +
+     geom_boxplot(width=0.2, alpha=0.8) +
+     scale_fill_brewer(palette="Set2") +
+     labs(title="Sequence Conservation by Gene Category",
+          y="Nucleotide Identity (%)", x="") +
+     theme_minimal(base_size=13) + theme(legend.position="none")
+   ggsave("Figure_Sequence_Identity.png", p2, width=8, height=6, dpi=300)
+   print(p2)
+ }
Warning message:
The `draw_quantiles` argument of `geom_violin()` is deprecated as of ggplot2 4.0.0.
ℹ Please use the `quantiles.linetype` argument instead.
This warning is displayed once per session.
Call lifecycle::last_lifecycle_warnings() to see where this warning was generated. 
<img width="1066" height="878" alt="image" src="https://github.com/user-attachments/assets/5ea96de2-f63a-4b65-9b86-44260b5610d8" />

> save(flab_annotations, ortholog_table, orthologs,
+      avic_core_flab, rhiz_up_flab, shared_all_flab, unique_genes_flab,
+      go_stol_avic, go_stol_rhiz, go_flab_avic, go_flab_rhiz,
+      go_comp_avic, go_comp_rhiz, all_cons,
+      file="cross_species_full_analysis.RData")
> cat("\n========================================\n")

========================================
> cat("CROSS-SPECIES ANALYSIS COMPLETE\n")
CROSS-SPECIES ANALYSIS COMPLETE
> cat("========================================\n")
========================================
> cat("Orthologs:", nrow(orthologs), "\n")
Orthologs: 15816 
> cat("Avicularium conservation:", round(100*length(avic_core_flab)/length(avic_core), 1), "%\n")
Avicularium conservation: 11.1 %
> cat("Rhizostol conservation:", round(100*length(rhiz_up_flab)/length(rhiz_up), 1), "%\n")
Rhizostol conservation: 23.2 %
> cat("Shared all conservation:", round(100*length(shared_all_flab)/length(shared_all), 1), "%\n")
Shared all conservation: 86.7 %
> cat("\nOutputs:\n")

Outputs:
> cat("  ortholog_table_annotated.csv\n")
  ortholog_table_annotated.csv
> cat("  cross_species_full_analysis.RData\n")
  cross_species_full_analysis.RData
> cat("  Figure_CrossSpecies_Conservation.png\n")
  Figure_CrossSpecies_Conservation.png
> cat("  Figure_Sequence_Identity.png\n")
  Figure_Sequence_Identity.png
