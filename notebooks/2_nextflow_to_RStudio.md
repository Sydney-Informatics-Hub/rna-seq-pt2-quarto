---
fig-cap-location: top
from: markdown+emoji
---


# **Setup RStudio on Nimbus VM**

<div class="objectives">  
### **Objectives**
- Introduction to RStudio
- How to open RStudio on the Pawsey training VM?
</div>  

<div class="questions">  
### **Questions**

- How to get the full gene count-matrix for downstream analysis?
- How to open RStudio on the Pawsey training VM?
- How to use count matrix to identify differentially expressed genes?
</div>  

## **R and RStudio**
- R is a programming language for statistical computing and graphics.
- RStudio is an integrated development environment which can be used to write and excecute R-code.


### **Using R/RStudio IDE for DE analysis**
- The gene-count matrix which was generated using the nefcore-rnaseq pipline can be used to perform statistical analyses and determine differentially expressed (DE) genes and pathways.
- Multiple independant packages/libraries have been developed in [R-programming](https://www.r-project.org/), which can be used for performing various kinds of 'omics' analysis. 
- R packages such as [DeSeq2](https://bioconductor.org/packages/release/bioc/html/DESeq2.html), [EdgeR](https://bioconductor.org/packages/release/bioc/html/edgeR.html) etc are used for identification of differencially expressed (DE) genes. Today we will be using DeSeq2.


## **Run RStudio on the Nimbus trainee VM**
This is a two step process

### **Step1: Run the rserver command (Pawsey Nimbus)**

```default
# Create a temporary rstudio-server  folder on your instance:
mkdir -p /tmp/rstudio-server

PASSWORD='abc' singularity exec -B /tmp/rstudio-server:/var/lib/rstudio-server -B /tmp/rstudio-server:/var/run/rstudio-server -B ~/base_directory/working_directory:/home /cvmfs/containers.biocommons.aarnet.edu.au/r/n/rnaseq_rstudio.sif rserver --auth-none=0 --auth-pam-helper-path=pam-helper --server-user ubuntu
```

::: {.callout-note appearance="simple"}
## No output is good output :grinning:
Once you paste the above command in the termonal window and press `Enter`, you SHOULD NOT see any output (the command prompt is stuck at the terminal, awaiting any further action!). If this happens, we are good to go.. 
:::


::: {.callout-note appearance="simple"}
## Feel good to use screen :grimacing:
You can also run the above command using a `screen` window.
:::



### **Step2: Open RStudio from a browser (Local machine)**
- Open up a browser window (__IMPORTANT__: Firefox does not work. Use Chrome or Safari.)
- Type `146.118.XX.XX:8787` in your browser where the XX.XX will be replaced by your IP specific digits. So if my login IP is 146.118.67.219, I will type `146.118.67.219 :8787` in the browser (e.g. `Chrome`) and press enter.
- Enter the username, which is your image operating system, which is `ubuntu`.
- Enter the password, which in this example is `abc`.
- Since you have entered the directory `~/base_directory/working_directory/`in the to bind-mount in the RStudio server command above, you can only see the path `~/base_directory/working_directory/rstudio` from your RStudio interface. Please transfer all inpout files to this path. 
- Run your R commands as you normally would. 
- To end the session, simply exit from the browser. To also end the session on your Nimbus instance, run the following: 

```default
lsof -ti:8787 | xargs kill -9
```

<div class="keypoints">
### **Key points**
- RStudio server can be run on the Nimbus VM instance. This allowes the user an end-to-end experience when analysing the RNA-seq data on the Pawsey resource.
</div>