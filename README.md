# Honors Thesis Data Analysis

This repository contains all the Python scripts used in the data analysis for the BYU Honors thesis entitled "REGULATION OF CELL CYCLE PROTEINS AT THE EXTREMES OF COPY NUMBER VARIATION IN CANCER". Figures not included in this repository are ones that were taken from other sources (ie. Fig 2, source Cornwell JA, et al., 2023; Fig 3, source GTEX)

## **Setup**

* download and install [Miniconda](https://docs.conda.io/projects/miniconda/en/latest/miniconda-install.html) if you don't already have it
* add conda to PATH (if necessary)
* create a new conda environment with the target by running `conda create --name &lt;env>` (replace `&lt;env>` with your desired environment name)
* activate the conda environment `conda activate &lt;env>`
* install the necessary conda packages manually if needed
    * Python 3.12.2 was the version used for this project.
    * The following script should install the appropriate packages:  \
`conda install python cptac=1.5.14 pandas=2.2.2 numpy=1.26.4 statsmodels=0.14.2 matplotlib=3.10.0 scipy=1.13.1`
    * The following versions of each package were used in this project:
        * cptac 1.5.14
        * pandas 2.2.2
        * numpy 1.26.4
        * statsmodels 0.14.2
        * matplotlib 3.10.0
        * scipy 1.13.1

## **Figures**

#### Total number of CNV events for individual tumor samples in the CPTAC database.  
&emsp;Script: `CNV_Totals_Figure.ipynb`  
&emsp;&emsp;The function `Compare_CNV_Totals()` takes a Pandas dataframe of CPTAC CNV data and a list of cancer types of interest.   
&emsp;&emsp;The dataframe of CNV data can be generated using the provided `Access_CPTAC()` function, which takes a CPTAC cancer datatype  
&emsp;&emsp;(ex. `cptac.Ov()`).  
&emsp;Example inputs:  
&emsp;&emsp;`cnv_df = Access_CPTAC(cptac.Ov())`  
&emsp;&emsp;`Compare_CNV_Totals(cnv_df,['ov','brca','pdac'])`  
  
#### Box plots of comparing RBL1 and RBL2 expression across cancer types.  
&emsp;Script: `Comparison_Across_CancerTypes_Figure.ipynb`  
&emsp;&emsp;The functions `Compare_Proteomics()` and `Compare_Transcriptomics()` takes a Pandas dataframe of CPTAC proteomics data or  
&emsp;&emsp;transcriptomics data respectively, a list of cancer types of interest, and the name of a protein.  
&emsp;&emsp;The dataframe can be generated using the provided `Access_CPTAC()` function, which takes a CPTAC cancer datatype  
&emsp;&emsp;(ex. `cptac.Ov()`) and a boolean value representing whether to retrieve transcriptomic data or proteomic data  
&emsp;&emsp;(`True` for transcriptomics, `False` for proteomics).  
&emsp;Example inputs:  
&emsp;&emsp;`tran_df = Access_CPTAC(cptac.Ov(),True)`  
&emsp;&emsp;`Compare_Proteomics(prot_df,['ov','brca','pdac'],'RBL1')`  
&emsp;&emsp;`Compare_Transcriptomics(tran_df,['ov','brca','pdac'],'RBL2')`  

#### Correlation graphs between RBL1 gene expression and protein expression in BRCA, GBM, OV, and PDAC data from CPTAC.  
&emsp;Script: `Correlation_Figures.ipynb`  
&emsp;&emsp;The functions `Get_RNA_Protein_Correlation()` and `Get_CNV_Protein_Correlation()` take cancer type string, a CPTAC cancer  
&emsp;&emsp;datatype (ex. `cptac.Ov()`), and the name of protein. It is important to note that LSCC does not have any transcriptomic   
&emsp;&emsp;data to use for the `Get_RNA_Protein_Correlation()` function.  
&emsp;Example inputs:  
&emsp;&emsp;`Get_RNA_Protein_Correlation('ov',cptac.Ov(),'RBL1')`  
&emsp;&emsp;`Get_CNV_Protein_Correlation('pdac',cptac.Pdac(),'RBL2')`  

#### Pearson correlation coefficients for gene expression vs protein expression.  
&emsp;Script: `Correlation_Figures.ipynb`  
&emsp;&emsp;Running the code as described above for previous figure generates Pearson correlation coefficients and P-values,  
&emsp;&emsp;which were compiled in a table for this figure.

#### Linear regression results for RBL1, RBL2, CDK4, and CDK6 against total CNV events.  
&emsp;Script: `Linear_Regression_Analysis.ipynb`  
&emsp;&emsp;The function `Get_Linear_Regress_Model()` takes the name of a protein and a Pandas dataframe of protein expression  
&emsp;&emsp;data (proteomic or transcriptomic). The dataframe can be generated using the function `Get_Protein_Clinical_Dat()`,  
&emsp;&emsp;which takes a CPTAC cancer datatype (ex. `cptac.Ov()`), the name of a protein, and a boolean value representing whether  
&emsp;&emsp;to retrieve transcriptomic data or proteomic data (`True` for proteomics, `False` for transcriptomics).  
&emsp;Example inputs:  
&emsp;&emsp;`prot_clin_df = Get_Protein_Clinical_Dat(cptac.Ov(),True)`  
&emsp;&emsp;`Get_Linear_Regress_Model(prot_clin_df,'RBL1')`  
