# XP-GWAS Power Simulation

This repository contains concept code and plotting code for a simulation-based power analysis of pooled XP-GWAS designs.

The simplified question motivating the analysis was:

> How many accessions per pool are enough to detect causal SNP effects?

In practice, this question is more complicated than a single sample-size calculation. Detection power depends on allele-frequency effect size, sequencing depth, number of genome-wide SNPs tested, number of causal SNPs, multiple-testing correction, and whether adding more accessions dilutes the allele-frequency contrast between resistant and susceptible pools.

This simulation explores whether expanded pools with more accessions can improve power to detect smaller or multiple causal SNP effects.

## Summary

The main comparison is between:

| Design | Resistant pool | Susceptible pool |
|---|---:|---:|
| Core pool | 11 accessions | 11 accessions |
| Expanded pool | 27 accessions | 31 accessions |

The central idea is that expanded pools may improve power by reducing biological sampling variance. However, adding more accessions may also weaken, or dilute, the allele-frequency difference between resistant and susceptible pools.

The main conclusion from these simulations is:

> Expanded pools can increase power to detect causal SNP effects if they do not dilute the resistance/susceptibility signal too much.

In other words, the practical question is not only:

```text
Should we add more samples?
```
but rather:

```text
Can we add more samples while preserving the allele-frequency contrast between resistant and susceptible pools?
```

## Main Results

The full simulation was run as SLURM batch jobs on an HPC cluster. The SLURM scripts are not included because they were cluster-specific, but the R Markdown file documents the simulation model and plotting workflow. For support on implementation in your own cluster, reach out using the contact info below!

The results summarized here are based on the full simulation grid run as SLURM batch jobs on an HPC cluster. 

The simulations suggest that expanded pools can improve power to detect causal SNPs compared with the smaller core pools, especially when the expanded pools retain most of the allele-frequency contrast between resistant and susceptible groups.

However, the benefit of adding more accessions depends strongly on signal dilution. When expanded pools retain a high proportion of the core-pool effect size, they generally show higher power. When the added accessions substantially dilute the resistant/susceptible allele-frequency difference, the expanded design can lose much of its advantage.

Overall, the results support the idea that expanded pools are useful when additional accessions increase sample size without strongly weakening the phenotype-associated allele-frequency difference.

The main tradeoff is:

```text
More accessions reduce biological sampling variance,
but signal dilution reduces the effective allele-frequency difference.
```

## Computational Workflow

The simulation code in this repository documents the model and analysis workflow. Small test runs can be executed locally by reducing the number of SNPs and simulation replicates.
```r
M_SNPS <- 50000
NSIM <- 50
```
The full simulation grid used for the final results was run as SLURM batch jobs on a high-performance computing cluster because the full parameter set was too computationally intensive to run interactively.
For the final analysis, the full simulation was run using SLURM batch jobs with larger settings, including:
```r
M_SNPS <- 300000
NSIM <- 2000
```
The SLURM jobs generated result CSV files, which were combined into a single results table and figures.

## Conclusion

This simulation was designed to evaluate how pool size affects power to detect causal SNPs in a pooled XP-GWAS design.

The results suggest that expanded pools can improve power by reducing biological sampling variance, especially when the expanded pools retain most of the allele-frequency contrast between resistant and susceptible groups. However, if adding more accessions substantially dilutes the signal, the benefit of larger pool size can be reduced or lost.

Overall, the simulations support using expanded pools when additional accessions still represent strong resistant and susceptible phenotype extremes. The results should be interpreted as exploratory power estimates under the assumptions of the simulation model, not as exact predictions for every XP-GWAS experiment.

## Author

Sam McNeill  
USDA-ARS  
Samuel.McNeill@usda.gov

## Contact

For questions, suggestions, or issues with the code, please open an issue in this GitHub repository.

## Citation

If you use or adapt this code, please cite this repository.

Suggested citation:

```text
McNeill, S. 2026. XP-GWAS Power Simulation: Simulation-based power analysis for pooled XP-GWAS designs. GitHub repository.
