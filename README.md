# 16S rRNA Workflow in R

A reproducible workflow analyzing 16S rRNA gene amplicon sequencing data in R. This is the reference pipeline I share with lab members and collaborators who are starting microbiome analyses.

The workflow assumes you're starting from a phyloseq object (post-DADA2) and walks through quality filtering, normalization, exploratory visualization, alpha and beta diversity, and PERMANOVA testing.
If you don't have a phyloseq object yet, start with the example_dada2.html file to generate one.

## View the rendered workflow

The cleanest way to see what this pipeline does is to open the rendered HTML report:

[**full_16S_workflow.html**](full_16S_workflow.html)

The HTML shows every step with code, output, and figures inline. 

## What's inside

| File | What it is |
| --- | --- |
| `full_16S_workflow.Rmd` | Main analysis pipeline (RMarkdown source) |
| `full_16S_workflow.html` | Rendered report with code, output, and figures |
| `example_dada2.html` | Companion: example DADA2 run for generating ASVs |
| `MonarchHillData230322.csv` | Example metadata file (small example dataset) |
| `2024_16S_Workflow.Rproj` | RStudio project file |
| `Literature/` | Reference papers and tutorials I drew from |

## Pipeline overview

1. **Load packages and data** — phyloseq, tidyverse, microViz, decontam, microbiome
2. **Evaluate data** — read distribution checks, prevalence filtering, contaminant removal
3. **Check covariates** — sample metadata sanity checks
4. **Data transformation** —  options, with trade-offs noted
5. **Explore taxonomy** — composition plots at multiple ranks
6. **Alpha diversity** — Shannon, Simpson, observed, Chao1 with group comparisons
7. **Beta diversity** — Bray-Curtis and UniFrac ordinations (PCoA, NMDS)
8. **PERMANOVA** — testing whether group differences explain community variation

## Running it yourself

If you want to re-run the workflow on your own phyloseq object:

```r
# Required packages
install.packages(c("tidyverse", "vegan", "ggrepel"))

# Bioconductor packages
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install(c("phyloseq", "decontam", "microbiome"))

# microViz from GitHub
install.packages("microViz", repos = c(davidbarnett = "https://david-barnett.r-universe.dev", getOption("repos")))
```

Then open `2024_16S_Workflow.Rproj` in RStudio and knit `full_16S_workflow.Rmd`.

Last tested on R 4.3 with phyloseq 1.46.

## Notes

This is a teaching and reference workflow that draws from other tutorials referenced within each step. The choices here reflect what I find useful as a starting point and what I cover with new students. 

