# Mapping Visual Latent Factors to Chemical Descriptors

*Post-hoc audit of the CNN visual embeddings vs. 2D RDKit descriptors.*

## Visual_1 vs Aromaticity (Spearman ρ = +0.68)
![Scatter Plot Visual 1](../phase4/visuals/visual_1_scatter.png)

This scatter plot demonstrates a strong positive correlation between the first visual latent factor (`Visual_1`) and the number of aromatic rings. The pre-trained CNN successfully learned to abstract aromaticity directly from the 2D molecular depictions, aligning with traditional cheminformatics descriptors.

## Visual_0 vs Molecular Size (Spearman ρ = -0.79)
![Scatter Plot Visual 0](../phase4/visuals/visual_0_scatter.png)

`Visual_0` exhibits a strong negative correlation with molecular size (Heavy Atom Count). This indicates that the CNN uses this latent axis to capture molecular compactness: larger, bulkier molecules yield lower `Visual_0` values.

<br>

---
[⬅️ Back to project README](../README.md)