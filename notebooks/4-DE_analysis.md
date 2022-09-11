---
fig-cap-location: top
font size: 2.5
---


## Create the DESeqDataSet object in DeSeq2

<div class="questions">  
### Questions
- How to create the DESeqDataSet object?
</div>

<div class="objectives">  
### Objectives
- Create a DESeqDataSet object with gene-count and experimental design information

</div>

#### **The DESeqDataSet object**
- A DESeqDataSet object must have an associated design formula. 
  - The design formula expresses the variables which will be used in modeling. 
  - The formula should be a tilde (`~`) followed by the variables with plus signs between them.
  - The design can be changed later, however then all differential analysis steps should be repeated, as the design formula is used to estimate the dispersions and to estimate the log2 fold changes of the model.
- There are multiple ways of constructing a DESeqDataSet, depending on what pipeline was used upstream of DESeq2 to generated counts or estimated counts
  - Here we have a matrix (as read in a dataframe above) of read counts prepared from our previous analysis using nfcore-rnaseq pipeline.
  - So we use have used the function - DESeqDataSetFromMatrix


```r
dds <- DESeqDataSetFromMatrix(countData = counttable,
                              colData = meta,
                              design = ~ condition)
```

In the above formula we have 
- A count matrix (countData) called counttable
- A table of sample information called meta.
- The design which defines the sample types as per the condition ; here `WT` and `KO`
- If we are controlling for batch differences then the design can be defined as design= ~ batch + condition.
- The two factor variables batch and condition should be columns of coldata.




#### **Pre-filtering of lowly expressed genes**
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

#### **Note:**

- Only 67% of the genes remain after performing this filtering step.
- This demonstrates the degree to which our performance will be improved by discarding the non-informative entries.

```r
[1] 19859
[1] 13412
```

#### **Explicitly set the factors levels**
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




<div class="keypoints">
### Key points

- We have used DeSeq2 to identify DE genes
</div>  