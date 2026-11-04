>📌 This is the public showcase repository for my specialization project UV-Curing Predictor.  
>**Source Code:** The full implementation is hosted in a private repository.
> Access is granted to recruiters and collaborators upon request.
> → [Request access](mailto:irene.ghioni@gmail.com?subject=Access%20request%20-%20UV-Curing%20Predictor)    
><br/>
>[![Source Code](https://img.shields.io/badge/Source_Code-Private-6e7681?style=for-the-badge&logo=github)](https://github.com/ireneghioni-glitch/AI-Powered-UV-Curing-Predictor-and-PI-Discovery)

# UV-Curing Predictor and Photoinitiator Discovery

[![Status](https://img.shields.io/badge/STATUS-WORK_IN_PROGRESS-F97316?style=for-the-badge&logo=statuspage&logoColor=white)](#)
[![Version](https://img.shields.io/badge/version-1.2.0-334155?style=for-the-badge)](https://github.com/ireneghioni-glitch/AI-Powered-UV-Curing-Predictor-and-PI-Discovery/releases/tag/v1.2.0)
[![Live Reflex App](https://img.shields.io/badge/Reflex_App-To_Be_Deployed-7C3AED?style=for-the-badge&logo=reflex&logoColor=white)](https://ai-powered-uv-curing-predictor.reflex.run)
[![Python 3.9.25](https://img.shields.io/badge/Python-3.9.25-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Conda](https://img.shields.io/badge/Conda-44A833?style=for-the-badge&logo=anaconda&logoColor=white)](https://docs.conda.io/)
[![XGBoost](https://img.shields.io/badge/XGBoost-Machine_Learning-2887D7?style=for-the-badge)](https://xgboost.readthedocs.io/)
[![RDKit](https://img.shields.io/badge/RDKit-Cheminformatics-3838FF?style=for-the-badge&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQBAMAAADt3eJSAAAABGdBTUEAALGPC/xhBQAAACBjSFJNAAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAAAFVBMVEXc3NwUFP8UPP9kZP+MjP+0tP////9ZXZotAAAAAXRSTlMAQObYZgAAAAFiS0dEBmFmuH0AAAAHdElNRQfmAwsPGi+MyC9RAAAAQElEQVQI12NgQABGQUEBMENISUkRLKBsbGwEEhIyBgJFsICLC0iIUdnExcUZwnANQWfApKCK4doRBsKtQFgKAQC5Ww1JEHSEkAAAACV0RVh0ZGF0ZTpjcmVhdGUAMjAyMjowMy0xMVQxNToyNjo0NyswMDowMDzr2J4AAAAldEVYdGRhdGU6bW9kaWZ5ADIwMjItMDMtMTFUMTU6MjY6NDcrMDA6MDBNtmAiAAAAAElFTkSuQmCC)](https://www.rdkit.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-Deep_Learning-DC2626?style=for-the-badge&logo=pytorch&logoColor=white)](https://pytorch.org/)
[![BeCode Bootcamp](https://img.shields.io/badge/BeCode-AI_%26_Data_Science-46C3C6?style=for-the-badge)](https://becode.org/)  
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](https://opensource.org/licenses/MIT)

An end-to-end, full-stack Machine Learning and Cheminformatics platform designed to predict polymerization conversion percentage (**% Double Bond Conversion**) for UV-curable formulations and enable virtual screening for novel Photoinitiator (PI) discovery. Built with a modular 5-phase data pipeline, computer vision feature extraction, XGBoost gradient boosting, and an interactive **Reflex** web application.

> **Status Notice: Ongoing Development** 
> This project is under active development. Version 1.2 introduces a completely overhauled, chemistry-validated molecular registry (56 PIs, 13 Monomers) and expands the PI photochemical taxonomy from 4 to 10+ distinct structural classes (including Acylgermanes, Titanocenes, and Thioxanthones). The compatibility classifier has been upgraded from Random Forest to an L1-penalized Logistic Regression, solving the curse of dimensionality. A poster presenting these results was presented at ChemAI Amsterdam (November 4, 2026).

* **Domain:** Cheminformatics, Photopolymer Chemistry, Computer Vision & Applied Machine Learning
* **Project Nature:** Solo Capstone Project
* **Frameworks & Stack:** Python, RDKit, MobileNetV2 (TensorFlow/Keras), PyTorch, XGBoost, Scikit-Learn, Reflex, SQLModel

<br>

> **Deployment Note:** Cloud deployment via Reflex Cloud is planned for the next iteration. The application currently runs locally and is fully reproducible by following the setup instructions below.

<p align="center">
  <img src="img/wip.gif" width="150" alt="work in progress">
</p>  
<p align="center">
    <i>I’m currently giving the app’s UI a fresh new look! A screenshot of it will be available here soon :)</i>
</p> 

---

## 📌 ChemAI 2026 Poster Support Materials
If you scanned the QR code on the poster, you can find the detailed visualizations here:
*   [📊 Scatter Plots: Mapping Visual Factors to Chemical Descriptors](poster_material/scatter_plots.md)
*   [🧪 Molecular Grids: Decoding Unmapped Latent Axes](poster_material/molecular_grids.md)

---

## Industrial Context & Note on Simulated Data

### The Industrial Bottleneck
In the formulation chemistry of UV-curable coatings, inks (3D printing, inkjet), and adhesives, achieving high double-bond conversion percentage ($\% \text{Conversion}$) is critical for mechanical strength, solvent resistance, and safety (preventing uncured monomer migration). However, experimental data on photoinitiator reactivity and industrial ink formulations are highly **proprietary and non-accessible** in public domains.

### Chemically Sound MVP Data Simulation
To overcome the lack of public experimental datasets while maintaining industrial relevance, the MVP dataset was generated using a **chemically and physically informed simulation engine:**

*   **Photoinitiator Photochemistry (Φ_cl channel):** The simulator dynamically reads a taxonomy of 10+ PI classes from an external YAML file (`data/pi_taxonomy.yaml`). Each class is assigned a literature-derived quantum efficiency (e.g., Acylphosphine oxides 0.85, α-Hydroxy ketones 0.55, Benzophenones 0.30, Co-initiators 0.00). This channel multiplies the kinetic progress independently of the solubility channel and is what makes the simulated target structurally photochemistry-dependent.
*   **Photoinitiator Solubility (LogP channel):** Wildman–Crippen LogP drives a phase-separation penalty in aqueous media: hydrophobic PIs ($LogP > 2$) precipitate and lose efficiency ("like dissolves like"). This channel is orthogonal to $Φ_cl$: a PI can be soluble but photochemically weak, or efficient but phase-separate.
*   **Monomer Reactivity & Steric Effects:** SMARTS-based detection of acrylate vs methacrylate motifs, functionality-weighted reactivity (tri-acrylates > di-acrylates > mono-acrylates > methacrylates), and α-methyl steric penalty for methacrylates.
*   **Diffusion-Controlled Vitrification Ceiling:** $α_{max}$ decreases with crosslink density (95% base, −6% per additional reactive group beyond the first). Multi-acrylates vitrify earlier, trapping radicals and halting the reaction.
*   **UV Dose & Concentration Kinetics:** First-order saturation curve for UV energy dose ($τ_{dose} = 250 mJ/{cm}^2$); Beer-Lambert inner-filter effect peaking at 3 wt% PI and decaying exponentially beyond.
*   **Deterministic Full-Factorial Design:** A **150,800-row** DoE (754 PI–monomer pairs × 200 process conditions) covers the grid `is_aqueous` × `pi_conc` (0.5–5.0 wt%) × `uv_dose` (100–1000 mJ/cm²). ***Note:*** $LogP$ is not a process variable: it is a molecular property, so it enters the target through the PI and monomer descriptors, not through the factorial grid.

> **Transferability to Real Lab Data:**  
> The entire architecture (from PubChem API ingestion and RDKit pre-processing to PCA dimensionality reduction and XGBoost inference) is engineered specifically to accept real laboratory experimental data (e.g., FTIR spectroscopy curing curves) without structural modifications.

---

## Architecture & System Data Flow

```text
                               +----------------------------------+
                               |       MOLECULE IDENTIFIERS       |
                               |    (Trade Names / CAS Numbers)   |
                               +----------------------------------+
                                                |
                                                v
                               +----------------------------------+
                               |     shared/pubchem_client.py     |
                               | - Cache Lookup                   |
                               | - YAML Fallback Dictionary       |
                               | - PubChem REST API (CID/SMILES)  |
                               +----------------------------------+
                                                |
                                                v
                               +----------------------------------+
                               |    shared/molecule_images.py     |
                               | - RDKit 2D Drawing Generation    |
                               | - Grayscale (224x224x1)          |
                               | - Augmentation (90°, 180°, 270°) |
                               +----------------------------------+
                                                |
                                                v
                               +----------------------------------+
                               | phase2/extract_embeddings_*.py   |
                               | - Pretrained MobileNetV2 (Frozen)|
                               | - Global Average Pooling         |
                               | - 1280-D Visual Fingerprint      |
                               +----------------------------------+
                                                |
                                                v
                               +----------------------------------+
                               |  DATASET REDUCTION & DoE ENGINE  |
                               | - 4-Rotation Augmentation Avg    |
                               | - PCA Compression (PI:55, Mono:12)|
                               | - Physics Simulation:            |
                               |     LogP + Φ_cl (10+ classes)    |
                               | - 754 pairs × 200 conditions     |
                               |   = 150,800-row factorial grid   |
                               +----------------------------------+
                                                |
                        +-----------------------+-----------------------+
                        |                                               |
                        v                                               v
       +----------------------------------+          +----------------------------------+
       |   phase4/train_xgboost.py        |          | phase4/train_compatibility_      |
       | - Tabular Concatenation          |          |        classifier.py             |
       | - XGBoost Regressor (Early Stop) |          | - Pair-level aggregation         |
       | - R² = 0.977, RMSE = 1.53%       |          |   (1,482 unique groups)          |
       | - Spearman ρ = 0.93              |          | - Logistic Regression L1         |
       | - Output: % Conversion           |          | - 4107-D Morgan FP vs 11 physical|
       +----------------------------------+          | - PR-AUC 0.845 vs 0.350          |
                        |                            +----------------------------------+
                        v                                               |
       +----------------------------------+                           v
       | xgboost_model.json               |          +----------------------------------+
       | pca_pi.pkl / pca_mono.pkl        |          | compatibility_classifier.pkl     |
       | model_config.json                |          | + audit report (docs/)           |
       +----------------------------------+          +----------------------------------+
                        |                                               |
                        +-----------------------+-----------------------+
                                                |
                                                v
                               +----------------------------------+
                               |       inference/pipeline.py      |
                               | - Lazy Singleton Models          |
                               | - Sub-Second Runtime Inference   |
                               +----------------------------------+
                                                |
                                                v
                               +----------------------------------+
                               |      app/ (Reflex Frontend)      |
                               | - Interactive Prediction UI      |
                               | - SQLModel Audit Logging         |
                               +----------------------------------+
```

> **Note on Phase 3 (PyTorch MLP baseline):**  
> A Multi-Layer Perceptron was trained in phase3/ as an educational baseline to compare tabular deep learning against XGBoost on this dataset. It is not part of the runtime pipeline: XGBoost proved superior on the 70+ dimensional tabular representation, and the MLP remains a pedagogical artifact. It can be ignored when tracing the production data flow.

### System Workflow
1. **SMILES Resolution (`shared/pubchem_client.py`):** Resolves commercial trade names or CAS Registry Numbers into canonical SMILES strings via a three-tier hierarchy (Cache CSV → Curated YAML Dictionary → PubChem REST API).
2. **Image Generation (`shared/molecule_images.py`):** RDKit renders 2D molecular structures into $224 × 224$ grayscale pixel grids with 4-fold rotational augmentation.
3. **Computer Vision Feature Extraction (`phase2/`):** Pass molecular images through a frozen pre-trained **MobileNetV2** backbone on ImageNet. Global Average Pooling extracts a 1280-dimensional visual embedding per image.
4. **Dimensionality Reduction & DoE Construction (`phase4/train_xgboost.py`):** Rotational augmentations are averaged per molecule. Principal Component Analysis (PCA) compresses 1280-D embeddings down to 55 components for PIs and 12 for monomers ($N-1$ full-rank). A deterministic full-factorial DoE then covers 754 PI–monomer pairs × 200 process conditions = **150,800 rows**.
5. **Physics-Informed Simulation:** Target conversion values are generated through a two-channel PI model. Channel 1 (solubility) applies a Wildman–Crippen LogP penalty in aqueous media. Channel 2 (photochemistry) multiplies the kinetic progress by the class-specific quantum efficiency $Φ_cl$ dynamically loaded from `pi_taxonomy.yaml`. These are combined with monomer reactivity, UV dose saturation, and Beer–Lambert shielding.
6. **Tabular Machine Learning (`phase4/train_xgboost.py`):** Concatenates 55 PI PCA + 12 monomer PCA + 3 process parameters (`Is_Aqueous`, `%PI`, `UV_Dose`) into a **72-dimensional** feature vector. Trains an **XGBoost Regressor** with validation-based early stopping, achieving $R^{2} = 0.977$, $RMSE = 1.53$\%, and a ranking fidelity (Spearman $\rho$) of **0.93**.
7. **Pair-Level Compatibility Classifier (`phase4/train_compatibility_classifier.py`):** The DoE is aggregated to 1,482 unique (PI, monomer, medium) groups. A **Logistic Regression with L1 penalty** is deployed to predict viable conversion (≥ 60%). L1 performs automatic feature selection, solving the curse of dimensionality (92 positives, 4,107 features). **Morgan Fingerprints (PR-AUC 0.845)** drastically outperform **11 physical descriptors (PR-AUC 0.350)**, demonstrating that *the molecular representation must follow the physics of the target.* Full audit in `docs/compatibility-audit.md`.
8. **Inference Pipeline & Reflex Web App (`inference/`, `app/`):** Exposes `predict()` with lazy singleton model loading and a reactive web dashboard.

---

## Technical Implementation & Pedagogical Choices

### 1. The Computer Vision Choice (Pedagogical vs. Production)
* **Educational Context:** Feeding 2D molecular structure drawings into a Convolutional Neural Network (MobileNetV2) was implemented specifically to fulfill the **Data Science specialization** requirements of the BeCode Bootcamp (**Deep Learning & Computer Vision** content).
* **Production Reflection:** In pure chemical informatics, molecular graph representations (GNNs) or direct 2D/3D QSAR descriptors are computationally more direct than image-based CNN embeddings.
* **Future Computer Vision Repurposing:** In future iterations, the Computer Vision module will be repurposed for physical laboratory images (e.g., contact angle sessile drop images for surface energy, optical microscopy), while chemical embeddings transition to direct QSAR and graph representations.

### 2. XGBoost vs. Deep Learning Neural Network
* **Phase 3 PyTorch Baseline:** A Multi-Layer Perceptron (MLP) was constructed in PyTorch as an educational baseline.
* **Phase 4 XGBoost Dominance:** XGBoost proved vastly superior for tabular integration of embeddings and environmental variables, capturing non-linear interactions and achieving $R^2 = 0.977$.

### 3. Random Forest vs. L1 Logistic Regression (The Classifier)
With 1,482 samples (only 92 positives) and 4,107 features, Random Forest overfits to noise (PR-AUC drops to 0.670). By switching to **Logistic Regression with L1 penalty (Lasso)**, we force the model to perform automatic feature selection. L1 zeroes out 3,982 irrelevant Morgan bits and isolates a stable core of **38 highly predictive features** across all CV folds. This unlocks the true potential of the structural fingerprints, raising the PR-AUC to **0.845**.

### 4. Software Engineering & MLOps Best Practices
* **Training/Inference Contract:** Identical preprocessing (4-rotation averaging and PCA transformation matrices saved via `joblib`) is applied at inference time to prevent silent feature distribution drift.
* **Single Source of Truth:** `data/entities.yaml` and `data/pi_taxonomy.yaml` decouple the molecule registry and the photochemical physics from the Python code, ensuring the pipeline is fully data-driven.
* **Fail-Fast SMARTS Matching:** `QSARFeatureExtractor` raises explicit errors if a molecule cannot be sanitized or if no SMARTS pattern matches, preventing silent data corruption during the simulation.

---

## 📁 Repository Structure

```text
AI-Powered-UV-Curing-Predictor-and-PI-Discovery/
├── app/                                  # Reflex web application
├── data/                                 # Master registries (entities.yaml, pi_taxonomy.yaml)
├── inference/                            # Runtime inference module
├── shared/                               # Shared reusable core client (RDKit, PubChem, QSAR)
├── phase1/                               # Phase 1: Ingestion & Image Generation
├── phase2/                               # Phase 2: CV Feature Extraction
├── phase3/                               # Phase 3: Deep Learning Core (Baseline)
├── phase4/                               # Phase 4: Tabular Integration & XGBoost
│   ├── train_xgboost.py                  # DoE, PCA & XGBoost training pipeline
│   ├── train_compatibility_classifier.py # L1 Logistic Regression classifier & audit
│   ├── generate_translation_card.py      # Post-hoc CNN latent factor audit
│   ├── plot_poster_feature_importance.py # A0 Poster-ready feature importance plot
│   ├── pca_pi.pkl / pca_mono.pkl         # Serialized PCA transformers
│   └── xgboost_model.json                # Serialized XGBoost model
├── docs/                                 # Project documentation & logs
├── requirements-training.txt             # Explicit Python dependencies for chemvision_env
├── requirements-app.txt                  # Explicit Python dependencies for reflex_env
└── README.md                             # Repository documentation
```

---

## Local Setup & Deployment
This project uses **two isolated Python environments** because the training pipeline and the web application have conflicting dependency constraints (notably NumPy 1.x vs 2.x, and Python 3.9 vs 3.11).

| Environment | Python | Purpose | Dependencies file |
|---|---|---|---|
| `chemvision` | 3.9 | Phases 1–4: data ingestion, embeddings, model training | `requirements-training.txt` |
| `reflex_app` | 3.11 | Phase 5: Reflex web application, runtime inference | `requirements-app.txt` |

### 1. Clone Repository
```bash
git clone https://github.com/ireneghioni-glitch/AI-Powered-UV-Curing-Predictor-and-PI-Discovery.git
cd AI-Powered-UV-Curing-Predictor-and-PI-Discovery
```

### 2. Set Up the Training Environment (`chemvision`)
```bash
conda create -n chemvision python=3.9 -y
conda activate chemvision
pip install -r requirements-training.txt
```

### 3. Set Up the Application Environment (`reflex_app`)
**Dual-Environment Isolation:** The training pipeline and the web application are deliberately isolated into two conda environments with different Python versions (3.9 and 3.11). This resolves a hard dependency conflict: the CNN backbone requires NumPy 1.x for RDKit compatibility, while the Reflex web stack requires NumPy 2.x. The dual-environment architecture mirrors the standard practice of separating offline training infrastructure from online serving infrastructure in production ML systems.
```bash
conda create -n reflex_app python=3.11 -y
conda activate reflex_app
pip install -r requirements-app.txt

# Node.js is required by Reflex to compile the frontend
conda install -c conda-forge "nodejs>=22.22" -y
```

### 4. Retrain the Model from Scratch  
Only needed if you want to regenerate `xgboost_model.json`, `pca_pi.pkl`, and `pca_mono.pkl` from raw data.  
```bash
conda activate chemvision

# Phase 1: fetch SMILES and generate molecular images
python -m phase1.fetch_molecules_PIs
python -m phase1.fetch_molecules_monomers
python -m phase1.generate_images_PIs
python -m phase1.generate_images_monomers

# Phase 2: extract CNN embeddings
python phase2/extract_embeddings_PIs.py
python phase2/extract_embeddings_monomers.py

# Phase 4: train XGBoost and L1 Classifier
python -m phase4.train_xgboost
python -m phase4.train_compatibility_classifier --audit
```

### 5. Initialize Database & Launch the App
```bash
conda activate reflex_app

# Initialize Reflex DB and apply migrations
reflex db init
reflex db makemigrations --message "initial schema"
reflex db migrate

# Launch the web application
reflex run
```
Navigate to `http://localhost:3000` in your browser.

> **NOTE**:
> First prediction takes ~8 seconds (TensorFlow + MobileNetV2 + XGBoost are loaded lazily on the first request). Subsequent predictions complete in under 1 second thanks to module-level singleton caching.

---

## Roadmap & Next Steps
The project follows a structured post-MVP roadmap detailed in the `docs/` repository files:

1. **QSAR Descriptor Integration - PARTIALLY IMPLEMENTED (`qsar-descriptor-integration-guide-en.md`):**  
✅ **Done:** SMARTS-based acrylate vs methacrylate detection, functionality-weighted reactivity, α-methyl steric penalty, Wildman-Crippen LogP solubility penalty, and the expanded 10+ class Φ_cl photochemical efficiency channel loaded from `pi_taxonomy.yaml`.  
⬜ **Pending:** Double Bond Density (DBD) per monomer, topological polar surface area (TPSA) on the monomer side, quantum-mechanical descriptors (HOMO/LUMO energies) for radical stability.  
2. **Simulation Engine Refinements:**
    - **Hybrid lab + simulated data:** When FTIR conversion curves become available, substitute the simulated target with the measured value.
    - **Ink/coating thickness:** Introduce cured-film thickness to couple with the Beer–Lambert inner-filter effect.
    - **Multi-PI formulations:** Generalize the simulator to compute conversion for PI blends (Type I / Type II synergy).
    - **$α_{max}$ for monomer blends:** Mixture-weighted $T_{g}$ model (Fox or Gordon–Taylor) rather than a linear crosslink counter.
    - **Configurable heuristic constants:** Externalize the remaining hardcoded coefficients in `simulate_conversion_qsar()` to a versioned config file.
3. **Learned Classifiers & Representation Alternatives:**
    - **PI photochemical class classifier:** Train a model to predict the $Φ_cl$ class directly from SMILES, replacing the literature lookup with a learned mapping.
    - **Morgan Fingerprints (2048-bit) + XGBoost as regression alternative:** Evaluate whether Morgan FP can match the CNN embeddings for the regression target. The CNN remains the pedagogical anchor; Morgan FP becomes a chemistry-native pipeline to compare.
4. **Dual-Model Formulation & Printing Window (`desired_prod_curing-and-formulation-prediction-pipeline.md`):**
Expanding into a dual-model system:  
    - **Model 1 (Printing/Jetting):** Predicts blend viscosity, surface tension, and calculates the Ohnesorge/Z-number printability window.
    - **Model 2 (Curing):** Predicts double-bond conversion and cured film $T_{g}$.
    - **Multi-Objective Optimization:** Integrating Optuna Bayesian optimization to discover optimal ink compositions.
5. **Active Learning & Generative Discovery (`post-mvp-roadmap.md`):**
    - **Active Learning:** Bayesian Optimization with UCB acquisition functions.
    - **Generative Modeling:** Variational Autoencoder (VAE) on SMILES for *in-silico* generation of novel photoinitiators.
    - **Closed-Loop Discovery:** Coupling generator, predictor, and acquisition function in an automated loop.
6. **Architecture & Engineering Enhancements:**
    - **Runtime Catalogue Management - PARTIALLY IMPLEMENTED:** ✅ `entities.yaml` is the single source of truth. ⬜ Pending: UI for write-back and autocomplete directly from PubChem.
    - **Config externalization - PARTIALLY IMPLEMENTED:** ✅ Molecule configuration and PI taxonomy are fully externalized. ⬜ Pending: Simulator constants (tau_dose, penalties, etc.) still need to be moved to YAML.
    - **SQLModel migration:** Migrating database models to pure SQLModel for Reflex 1.0 compatibility.
    - **Embedding Interpretability & Visualization - PARTIALLY IMPLEMENTED:** ✅ `phase4/generate_translation_card.py` and `phase4/audit_latent_factors.py` run post-hoc Spearman/Kruskal-Wallis tests, mapping latent axes to RDKit descriptors and generating molecular grids. ⬜ Pending: 2D UMAP projection of embeddings.
    - **Ecosystem integration:** Synthesis-route chatbot for newly discovered PIs.
7. **User Interface & UX Optimization:**  
    - **First-prediction latency:** ~8 s cold start. Improvement: warm up lazy singletons on app startup.
    - **Minimal error feedback:** Distinguish between "molecule not found", "invalid input", and network errors.
    - **No prediction history view:** Expose the curinglog table via a `/history` page.
    - **No input autocomplete:** Populate a dropdown from the existing molecule CSVs.
    - **No responsive layout / dark mode:** Add `rx.desktop_only` and a dark theme toggle.
8. **Beyond CNN Embeddings - Graph and Transformer Architectures (Exploratory):**  
    - **Graph Neural Networks (GNNs):** PyTorch Geometric, DGL.
    - **Pre-trained Chemical Transformers:** ChemBERTa, MolFormer.
    - **Generative Molecular Architectures:** VAEs and diffusion models on SMILES for de novo photoinitiator design.
9. **Learning & Reference Material:**  
[**TeachOpenCADD**](https://github.com/volkamerlab/teachopencadd): the reference notebook series for cheminformatics + ML.

None of these items blocks the functional MVP, but together they represent the gap between a working prototype and a product that a formulation chemist would use daily without friction.

<br>

## Changelog

### v1.2.0 — 2026-11-04
Major chemistry validation and ML architecture overhaul for ChemAI Poster.

- **Expanded Molecular Registry:** `entities.yaml` now contains **56 PIs** and **13 Monomers**. Corrected critical SMILES errors (e.g., TMPTA, PETA, Irgacure 907) and added out-of-domain test molecules (Titanocenes, Acylgermanes) for structural diversity.
- **Expanded Photochemical Taxonomy:** `pi_taxonomy.yaml` implements a 10+ class structural hierarchy (up from 4). The simulator dynamically loads $\Phi_{cl}$ values from this YAML via SMARTS matching.
- **Dataset Expansion:** DoE size increased to **754 PI–monomer pairs × 200 conditions = 150,800 rows**.
- **Regressor Update:** XGBoost retrained on the expanded dataset. Achieves **R² = 0.977, RMSE = 1.53%**, and a Spearman rank correlation of **0.93**.
- **Classifier Architecture Shift:** Replaced Random Forest with **Logistic Regression L1**. L1 performs automatic feature selection (zeroing out 3,982 features) to solve the curse of dimensionality.
- **Classifier Results:** On the 1,482 pair-level dataset, **Morgan Fingerprints achieve PR-AUC 0.845**, vastly outperforming the 11-physical-descriptor baseline (PR-AUC 0.350).
- **Interpretability Audit:** Added `generate_translation_card.py` to map CNN latent factors to RDKit descriptors and generate molecule grid visualizations.

### v1.0.0 — 2026-10-27
Second pipeline iteration: photochemistry-aware simulation and pair-level compatibility classifier.

- **Physics:** Added the **Φ_cl photochemical efficiency channel** to the simulation engine (acylphosphine 0.85 / benzoyl 0.60 / Type II 0.45 / co-initiator 0.00, literature-sourced from Fouassier and Decker). The simulator now models PI efficiency through two independent channels: LogP (solubility) and Φ_cl (photochemistry).
- **Dataset:** DoE restructured to **520 PI–monomer pairs × 200 process conditions = 104,000 rows**. LogP is no longer a factorial variable: it is a molecular property, not a process parameter, and the previous grid conflated the two.
- **Compatibility classifier:** Pair-level Random Forest pre-screening filter (`phase4/train_compatibility_classifier.py`), aggregated to 1,020 unique (PI, monomer, medium) groups by max conversion across process windows. **Morgan Fingerprints (4107-D) reach PR-AUC 0.770, overtaking the 11-physical-descriptor baseline at 0.739** (random baseline = 0.084). This is the central result: the representation must follow the physics of the target.
- **Interpretability audit:** Post-hoc analysis of the CNN latent factors (`docs/latent_factors_audit.md`, `phase4/audit_latent_factors.py`). Spearman ρ maps `Visual_0` → molecular size (+0.84), `Visual_1` → aromaticity (+0.51), `Visual_2` → ring topology (−0.45). Kruskal–Wallis across Φ_cl classes is inconclusive at this dataset size (n = 3 acylphosphines); analysis is documented as suggestive, not conclusive.
- **Literature mining:** BERTopic topic model on the UV-curing corpus (`phase4/train_bertopic.py`, 9 topics), persisted as interactive HTML in `phase4/visuals/`.
- **Regressor metrics:** XGBoost R² = **0.978**, RMSE = **1.49%** (previous v1.0.0: R² = 0.9860, RMSE = 1.58% on the older DoE). The slight decrease is expected — the target now depends on photochemical structure, which is a harder signal than solubility alone.
- **Feature contract:** 63-dimensional feature vector (51 PI PCA + 9 monomer PCA + 3 process parameters: `Is_Aqueous`, `%PI`, `UV_Dose`). The previous 4th process parameter (LogP) has been correctly moved out of the grid.
- **Documentation:** `data_flow_completed.md` reflects the two-channel physics, the 104k DoE, and the pair-level classifier. `compatibility-audit.md` and `latent_factors_audit.md` added to `docs/`.

### v1.0.0 — 2026-10-27
Second pipeline iteration: photochemistry-aware simulation and pair-level compatibility classifier.

- **Physics:** Added the **Φ_cl photochemical efficiency channel** to the simulation engine (acylphosphine 0.85 / benzoyl 0.60 / Type II 0.45 / co-initiator 0.00).
- **Dataset:** DoE restructured to 520 PI–monomer pairs × 200 process conditions = 104,000 rows. LogP removed from the factorial grid.
- **Compatibility classifier:** Pair-level Random Forest pre-screening filter. Morgan Fingerprints (4107-D) reach PR-AUC 0.770, overtaking the 11-physical-descriptor baseline at 0.739.
- **Regressor metrics:** XGBoost R² = 0.978, RMSE = 1.49%.

<br>

## License

This project is licensed under the MIT License. You are free to use, modify,
and distribute this software, provided that the original copyright notice
is included. See the `LICENSE` file for details.

<br>
<br>

---

<br>

#### Author
**Irene Ghioni**  
[AI & Data Science](https://becode.org/en/job-seekers/trainings/ai-data-science) Trainee at [BeCode Belgium](https://becode.org/) *(Specializing in Data Science)*   
R&D | Formulation | Materials Science | UV-Curing | Inks & Coatings  
[![LinkedIn Profile](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ireneghioni/) [![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white)](https://github.com/ireneghioni-glitch)
