# Decoding Unmapped Latent Axes: What does the CNN "see"?

*Post-hoc visualization of molecules with the HIGHEST and LOWEST values for specific CNN PCA components.*

## Unmapped Latent Axes (Steric/3D effects)

*These unmapped features capture geometric pixel patterns that standard 2D RDKit descriptors miss.*

### Visual_15 ▲ (Top XGBoost Feature) ↔ `Topological Complexity`
![Visual_15 Grid](../phase4/visuals/visual_15_grid.png)
* **HIGH:** Dense, complex, heteroatom-rich, and rigid frameworks (e.g., Irgacure 907, Camphorquinone, 9,10-Phenanthrenequinone). 
* **LOW:** Simpler, less structurally dense, or purely hydrocarbon frameworks (e.g., DABCO, Ivocerin, Anthracene).

### Visual_29 ↔ `Linear Elongation` & `Local Sterics`
![Visual_29 Grid](../phase4/visuals/visual_29_grid.png)
* **HIGH:** Extended, linear structures or prominent protruding side aliphatic chains (e.g., Omnirad TPO-L, Irgacure 907, TEA).
* **LOW:** Compact, highly branched, star-shaped, or planar molecules (e.g., Methylene Blue, TMPMP, DIPEA).

### Visual_43 ↔ `Terminal Group Extension`
![Visual_43 Grid](../phase4/visuals/visual_43_grid.png)
* **HIGH:** Molecules with distinct terminal functional groups projecting outward from a central core (e.g., 9,10-Phenanthrenequinone, DMAB, Omnirad 4MBZ).
* **LOW:** Highly fused blocks or symmetric structures where terminal groups are less visually distinct (e.g., Perylene, Darocur 1173, MDB).

### Visual_5 ↔ `Cyclic Framework`
![Visual_5 Grid](../phase4/visuals/visual_5_grid.png)
* **HIGH:** Presence of closed rings and dense cyclic frameworks (e.g., Methylene Blue, Irgacure 784, Irgacure 907).
* **LOW:** Open-chain aliphatic structures (thiols) with no cyclic features (e.g., PETMP, TMPMP, HDT).

---

## Mapped Latent Axes (Known Chemistry Confirmation)

*While the unmapped features demonstrate the CNN's ability to capture latent spatial information, these mapped components serve as a direct validation of its visual learning. The network successfully recovers fundamental chemical axes that align with standard physicochemical descriptors, proving it 'sees' structural properties as traditional cheminformatics tools.*

### Visual_1 ★ ↔ `Aromaticity`
![Visual_1 Grid](../phase4/visuals/visual_1_grid.png)
* **HIGH:** Highly conjugated aromatic systems with multiple benzene rings (e.g., Omnirad BAPO, Benzoin ether).
* **LOW:** Linear aliphatic chains lacking any aromatic rings (e.g., 2-Mercaptoethanol, Thioglycolic acid).

### Visual_0 ★ ↔ `Molecular Size`
![Visual_0 Grid](../phase4/visuals/visual_0_grid.png)
* **HIGH:** Small, compact molecules with lower molecular weight (e.g., DABCO, DIPEA).
* **LOW:** Large, extended molecules with high molecular weight and long chains (e.g., Esacure 1001M, Omnirad PBZ).

<br>

---
[⬅️ Back to project README](../README.md)