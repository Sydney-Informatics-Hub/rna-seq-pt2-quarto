---
title: "Differential expression analysis using DeSeq2"
teaching: 10
exercises: 0
questions:
- "How to use the DESeq2 module to perform differential expression (DE) analysis?"
- "How to visualise the results from DeSeq2 analysis?"



objectives:
- "Generate a list of differentially expressed genes."
- "Use visualisation techniques to analyse the results."

keypoints:
- We have used DeSeq2 to identify DE genes.
- 

---



#### Differential expression using the DESeqDataSet object
- A DESeqDataSet object must have an associated design formula. 
  - The design formula expresses the variables which will be used in modeling. 
  - The formula should be a tilde (~) followed by the variables with plus signs between them.
  - The design can be changed later, however then all differential analysis steps should be repeated, as the design formula is used to estimate the dispersions and to estimate the log2 fold changes of the model.
- There are multiple ways of constructing a DESeqDataSet, depending on what pipeline was used upstream of DESeq2 to generated counts or estimated counts
  - Here we have a matrix (as read in a dataframe above) of read counts prepared from our previous analysis using nfcore-rnaseq pipeline.
  - So we use have used the function - DESeqDataSetFromMatrix


```r
dds <- DESeqDataSetFromMatrix(countData = counttable,
                              colData = meta,
                              design = ~ condition)
```
In the above formula we have a : 
- The count matrix (countData) called counttable 
- A table of sample information called meta. 
- The design which defines the sample types as per the condition ; here ```WT``` and ```KO```



### Pre-filtering of lowly expressed genes
- Our count matrix may contain many rows with only zeros, and additionally many rows with only a few fragments in total
- Pre-filtering of such genes with very low counts is useful because: 
- Genes with very low counts across all samples provide little evidence for differential expression and they interfere with some of the statistical approximations that are used later in the pipeline.
- They also add to the multiple testing burden when estimating false discovery rates, reducing power to detect differentially expressed genes. 


```r
# How many gene rows before filtering?
nrow(dds)

keep <- rowSums(cpm(counttable)>1) >=4
dds <- dds[keep,]

# How many gene rows after filtering?
nrow(dds)

```
**Note**: 
- Only 67% of the genes remain after performing this filtering step.
- This demonstrates the degree to which our performance will be improved by discarding the non-informative entries.
```
[1] 19859
[1] 13412
```

#### Explicitly set the factors levels 
- By default, R will choose a reference level for factors based on alphabetical order.
- So if you never tell the DESeq2 functions which level you want to compare against (e.g. which level represents the control group), the comparisons will be based on the alphabetical order of the levels.
- Setting the factor levels can be done in two ways:


```r
# Using factor
#dds$condition <- factor(dds$condition, levels = c("Wild","KO"))
#OR

# using relevel, just specifying the reference level:
dds$condition ~ relevel(dds$condition, ref="Wild")
```


### Differential expression analysis

#### The DESeq function
```r

dds <- DESeq(dds)
res <- results(dds)



# padj 0.05
res_padj0.05<-results(dds,alpha=0.05)
summary(res_padj0.05)
resSig005_subset<-subset(res_padj0.05, padj < 0.05)
write.table(resSig005_subset, "res_DeSeq2_FDR0.05_comparison_Wild_vs_KO_FUllMatrix.tab", sep="\t", col.names=NA, quote=F)

# padj 0.1
res_padj0.1<-results(dds,alpha=0.1)
summary(res_padj0.1)
resSig01_subset<-subset(res_padj0.1, padj < 0.1)
write.table(resSig01_subset, "res_DeSeq2_FDR0.1_comparison_Wild_vs_KO_FUllMatrix.tab", sep="\t", col.names=NA, quote=F)

# Writing normalized counts
normalised_counts<-counts(dds,normalized=TRUE)
write.table(normalised_counts, "normalised_all_samples_DeSeq2_FUllMatrix.tab", sep="\t", col.names=NA, quote=F)

```



Should we plot some DE genes?

### Plot dispersion estimates
```r
plotDispEsts(dds, ylim = c(1e-6,1e3) )
```

### Tidy and annotate results
- Ordering by padj value
- Get gene names for ensembl IDs.

```r
# https://github.com/stephenturner/annotables
# grch38 comes from library(annotables)
res_tidy.DE = tidy.DESeqResults(resSig005_subset)
res_tidy.DE <- res_tidy.DE %>% arrange(p.adjusted) %>% inner_join(grcm38, by = c(gene = "symbol")) %>% dplyr::select(gene,baseMean, estimate, stderror, statistic, p.value, p.adjusted) 
#res_tidy.DE
```

### Volcano plot
- A volcano plot can help us summarise the differential expression of gene for our analysis.
- The y-axis shows -log10(adjusted-p-value) while the X-axis shows logFC of all genes.
- The default colour coding highlights the statistically significant genes and further those with a specific logFC cutoff.

```r
EnhancedVolcano(res_tidy.DE,
    lab = res_tidy.DE$gene,
    x = 'estimate',
    y = 'p.value',title = "Volvcano plot - WT versus KO",
    pointSize = 1.0,
    labSize = 5.0,
    pCutoff = 10e-16,
    FCcutoff = 1.5)

```
  <p align="center">
  <img src="{{ page.root }}/fig/volcano_plot.png" style="margin:10px;height:350px"/>
  </p>


