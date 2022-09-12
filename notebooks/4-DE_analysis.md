---
fig-cap-location: top
font size: 2.5
---


## Create the DESeqDataSet object in DeSeq2

<div class="questions">  
### **Questions**
- How to create the DESeqDataSet object?
</div>

<div class="objectives">  
### **Objectives**
- Create a DESeqDataSet object with gene-count and experimental design information

</div>

#### **The DESeqDataSet object**
- For performing differential expression analysis, the DESeqDataSet object must have an associated design formula. 
  - The design formula expresses the variables which will be used in modeling. 
  - The formula should be a tilde (`~`) followed by the variables with plus signs between them.
  - The design can be changed later, however then all differential analysis steps should be repeated, as the design formula is used to estimate the dispersions and to estimate the log2 fold changes of the model.
- There are multiple ways of constructing a DESeqDataSet, depending on what pipeline was used upstream of DESeq2 to generated counts or estimated counts
  - Here we have a matrix (as read-in a dataframe) of read counts. This is generated using the `nfcore-rnaseq pipeline`.
  - So we use use the function - DESeqDataSetFromMatrix


```r
dds <- DESeqDataSetFromMatrix(countData = counttable,
                              colData = meta,
                              design = ~ condition)
```

In the above formula we have 
<br>**1)** A count matrix (countData) called counttable
<br>**2)** A table of sample information called meta.
<br>**3)** The design which defines the sample types as per the condition ; here `WT` and `KO`
<br>Also, if we are controlling for batch differences then the design can be defined as design= ~ batch + condition.


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
### **Key points**
The object class used by the DESeq2 package to store the read counts and the intermediate estimated quantities during statistical analysis is the `DESeqDataSet`.
</div>  