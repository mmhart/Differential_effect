# Differential establishment, proliferation, and host responses of arbuscular mycorrhizal fungi

This repository contains the R scripts used to analyze data for the manuscript:

**Differential establishment, proliferation, and host responses among arbuscular mycorrhizal fungal inoculants**

The study examined how arbuscular mycorrhizal fungal (AMF) identity, host plant identity, and soil nutrient availability influence:

- Inoculant establishment
- Fungal abundance
- Root biomass mycorrhizal response
- Shoot biomass mycorrhizal response
- Shoot phosphorus mycorrhizal response

AMF establishment and abundance were quantified using isolate-specific digital droplet PCR (ddPCR).

## Repository structure

```
Data/
    ddpcr.csv
    MR_biomass_TotP_shoot_may25.csv

Scripts/
    01_AMF concentration roots and soil
    02_Bionomial Roots and Soil
    03_Stats all host
    04_AMF_Heatmap


## Statistical analyses

### 1. Soil establishment

Response:

```
present = copy_g_soil > 0
```

Model:

```
present ~ AMF + Plant + Nutrient
```

followed by isolate-specific models

```
present ~ Plant * Nutrient
```

using bias-reduced logistic regression (`brglm2`).

---

### 2. Root establishment

Response:

```
present = copy_g_root > 0
```

Model:

```
present ~ AMF + Plant + Nutrient
```

followed by isolate-specific analyses.

---

### 3. Soil abundance

Positive detections only (`copy_g_soil > 0`).

Response:

```
log10(copy_g_soil)
```

Model:

```
log10(copy_g_soil) ~ AMF + Plant + Nutrient
```

Type II ANOVA was used for fixed-effect inference.

---

### 4. Root abundance

Positive detections only (`copy_g_root > 0`).

Response:

```
log10(copy_g_root)
```

Model:

```
log10(copy_g_root) ~ AMF + Plant + Nutrient
```

followed by isolate-specific

```
Plant * Nutrient
```

models.

---

### 5. Plant mycorrhizal responses

Responses:

- Root biomass mycorrhizal response (MR)
- Shoot biomass MR
- Total shoot phosphorus MR

Model:

```
MR ~ AMF * Plant * Nutrient
```

Gaussian linear models were used for primary inference.

Estimated marginal means were calculated using the **emmeans** package.

---

## Software

Analyses were performed using **R (version 4.5.x)**.

Required packages:

- tidyverse
- car
- emmeans
- brglm2
- glmm.hp
- nlme
- patchwork

---

## Input files

### ddpcr.csv

Contains isolate-specific digital droplet PCR estimates of AMF abundance in soil and roots.

Primary variables include:

- AMF
- Plant
- Nutrient
- copy_g_soil
- copy_g_root

### MR_biomass_TotP_shoot_may25.csv

Contains calculated mycorrhizal response variables for:

- Root biomass
- Shoot biomass
- Total shoot phosphorus

---

## Outputs

Each workflow exports:

- Model summaries
- ANOVA tables
- Estimated marginal means
- Pairwise comparisons
- Diagnostic summaries
- Publication-quality figures
- Supplementary data tables (.csv)

Session information is saved for each workflow to ensure computational reproducibility.

---

## Reproducibility

All analyses can be reproduced by running the scripts in numerical order.

No manual editing of intermediate files is required.

---

## Citation

If you use these scripts or data, please cite the associated manuscript.

---

## License

This repository is distributed under the **MIT License**.
