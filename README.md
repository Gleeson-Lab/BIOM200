## BIOM200 Human genetics and genomics module
<br/>

Originaly created by Kyle Gaulton, Assistant Professor, Department of Pediatrics

kgaulton@ucsd.edu



Edited by Arzoo Patel for Joe Gleeson, Professor, Department of Neurosciences

<br/><br/>

##  Getting started

SSH into your account on TSCC (ssh username@login-tscc.sdsc.edu)

Note: some of you might not have a TSCC accout or might not be able to login to it. If you use Linux or Mac just open your terminal and continue to cloning the repository. If you have Windows you'll need a program to run bash shell on, such as [WSL](https://ubuntu.com/wsl)

<br/><br/>

Clone this repository into your home directory on TSCC, i.e.:

```
git clone https://github.com/Gleeson-Lab/BIOM200.git
```

<br/><br/>


## Exercise - prioritize clinically-significant variants from a human exome

The goal of this exercise is to identify potential pathogenic variants from human exome sequencing.

The Exome data you will annotate is in the repository you cloned here:
**Exome VCF**: `~/BIOM200/data/hu82436A.vcf.gz`

And you will annotate this exome using data on pathogenic variants from ClinVar:  
**ClinVar VCF**: `~/BIOM200/data/clinvar_20190909.vcf.gz`

Download VCFanno in order to functionally annotate variants
  
  Either download executable directly: 
  
  ```
  wget https://github.com/brentp/vcfanno/releases/download/v0.3.2/vcfanno_linux64 -O vcfanno
  ```
    
  Make sure that you have permissions to run the program:
  
  ```
  chmod +x vcfanno
  ```
  
  Or install with conda:
 
  ```
  conda install -c bioconda vcfanno
  ```
  
  

Run VCFanno to annotate exome with ClinVar, and ExAC and 1000 Genomes allele frequencies, using config file 'biom_config.toml' (there might be several 'warnings' but should still produce the correct output).  Make sure you are in your home directory when running this command

  ```
  vcfanno BIOM200/biom_config.toml BIOM200/data/hu82436A.vcf.gz > hu82436A.annot.vcf
  ```

This will add several columns to the INFO field of the VCF in the resulting annotated file 'hu82436A.annot.vcf', including: clinical_significance (benign, pathogenic, etc.), clinical_class (type of variant - snp, deletion, etc.), exac_allele_freq (allele frequency in ExAC), tgp_allele_freq (allele frequency in 1000 Genomes)

From this annotated VCF, extract all variants with `clinical_significance=Pathogenic`, and determine whether or not they are also present in ExAC or 1000 Genomes and what their allele frequencies are (if there is no 'exac_allele_freq' or 'tgp_allele_freq' info tag then it isn't in these databases)

**Questions**: 
1.  How many rare, likely pathogenic variants does this individual carry? 
2.  What types of variants are they (i.e. what changes do they make to the protein)? 
3.  What genes are they in, and what diseases do these variants cause?  

##  Potentially helpful commands

`grep` - extract information from a file 

`more` - view beginning of a file (hit spacebar scroll through more)

`ls` - list contents of a directory


