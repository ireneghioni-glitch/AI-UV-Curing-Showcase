>📌 This is the public showcase repository for my specialization project UV-Curing Predictor.  
>**Source Code:** The full implementation is hosted in a private repository.
> Access is granted to recruiters and collaborators upon request.
> → [Request access](mailto:irene.ghioni@gmail.com?subject=Access%20request%20-%20UV-Curing%20Predictor)    
><br/>
>[![Source Code](https://img.shields.io/badge/Source_Code-Private-6e7681?style=for-the-badge&logo=github)](https://github.com/ireneghioni-glitch/AI-Powered-UV-Curing-Predictor-and-PI-Discovery)

# UV-Curing Predictor and Photoinitiator Discovery

[![Status](https://img.shields.io/badge/STATUS-WORK_IN_PROGRESS-F97316?style=for-the-badge&logo=statuspage&logoColor=white)](#)
[![Version](https://img.shields.io/badge/version-1.1.0-334155?style=for-the-badge)](https://github.com/ireneghioni-glitch/AI-Powered-UV-Curing-Predictor-and-PI-Discovery/releases/tag/v1.0.0)
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
> This project is under active development. Version 1.1 adds the photochemical Φ_cl efficiency channel to the simulation engine and a pair-level PI–monomer compatibility classifier to the training pipeline. The roadmap now focuses on active learning, generative photoinitiator discovery, and graph/transformer molecular encoders. A poster presenting the Φ_cl-driven representation shift will be shown at ChemAI Amsterdam (November 4, 2026).

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

## Industrial Context & Note on Simulated Data

### The Industrial Bottleneck
In the formulation chemistry of UV-curable coatings, inks (3D printing, inkjet), and adhesives, achieving high double-bond conversion percentage ($\% \text{Conversion}$) is critical for mechanical strength, solvent resistance, and safety (preventing uncured monomer migration). However, experimental data on photoinitiator reactivity and industrial ink formulations are highly **proprietary and non-accessible** in public domains.

### Chemically Sound MVP Data Simulation
To overcome the lack of public experimental datasets while maintaining industrial relevance, the MVP dataset was generated using a **chemically and physically informed simulation engine:**

* **Photoinitiator Photochemistry (Φ_cl channel):** Each PI is assigned a quantum efficiency class drawn from the literature (Fouassier, Photoinitiation, Photopolymerization, and Photocuring, Hanser 1995; Decker, Prog. Polym. Sci. 21, 593, 1996): acylphosphine oxides Φ_cl = 0.85 (TPO, BAPO), benzoyl ketones Φ_cl = 0.60 (Irgacure 184, 651), Type II Φ_cl = 0.45 (benzophenones, thioxanthones), co-initiators Φ_cl = 0.00 (amines, thiols — no initiation without a PI partner). This channel multiplies the kinetic progress independently of the solubility channel and is what makes the simulated target structurally photochemistry-dependent.

* **Photoinitiator Solubility (LogP channel):** Wildman–Crippen LogP drives a phase-separation penalty in aqueous media: hydrophobic PIs ($LogP > 2$) precipitate and lose efficiency ("like dissolves like"). This channel is orthogonal to $Φ_cl$: a PI can be soluble but photochemically weak, or efficient but phase-separate.

* **Monomer Reactivity & Steric Effects:** SMARTS-based detection of acrylate vs methacrylate motifs, functionality-weighted reactivity (tri-acrylates > di-acrylates > mono-acrylates > methacrylates), and α-methyl steric penalty for methacrylates.

* **Diffusion-Controlled Vitrification Ceiling:** $α_{max}$ decreases with crosslink density (95% base, −6% per additional reactive group beyond the first). Multi-acrylates vitrify earlier, trapping radicals and halting the reaction.

* **UV Dose & Concentration Kinetics:** First-order saturation curve for UV energy dose ($τ_{dose} = 250 mJ/{cm}^2$); Beer-Lambert inner-filter effect peaking at 3 wt% PI and decaying exponentially beyond.

* **Deterministic Full-Factorial Design:** A $104,000$-row DoE ($520$ PI–monomer pairs × $200$ process conditions) covers the grid `is_aqueous` × `pi_conc` (0.5–5.0 wt%) × `uv_dose` (100–1000 mJ/cm²). ***Note:*** $LogP$ is not a process variable: it is a molecular property, so it enters the target through the PI and monomer descriptors, not through the factorial grid.

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
                               | - Manual Verified Dictionary     |
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
                               | - PCA Compression (PI:51, Mono:9)|
                               | - Physics Simulation:            |
                               |     LogP (solubility) + Φ_cl     |
                               | - 520 pairs × 200 conditions     |
                               |   = 104,000-row factorial grid   |
                               +----------------------------------+
                                                |
                        +-----------------------+-----------------------+
                        |                                               |
                        v                                               v
       +----------------------------------+          +----------------------------------+
       |   phase4/train_xgboost.py        |          | phase4/train_compatibility_      |
       | - Tabular Concatenation          |          |        classifier.py             |
       | - XGBoost Regressor (Early Stop) |          | - Pair-level aggregation         |
       | - R² = 0.978, RMSE = 1.49%       |          |   (1,020 unique groups)          |
       | - Output: % Conversion           |          | - RandomForest classifier        |
       +----------------------------------+          | - 4107-D Morgan FP vs 11 physical|
                        |                            | - PR-AUC 0.770 vs 0.739          |
                        v                            +----------------------------------+
       +----------------------------------+                           |
       | xgboost_model.json               |                           v
       | pca_pi.pkl / pca_mono.pkl        |          +----------------------------------+
       | model_config.json                |          | compatibility_classifier.pkl     |
       +----------------------------------+          | + audit report (docs/)           |
                        |                            +----------------------------------+
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
> A Multi-Layer Perceptron was trained in phase3/ as an educational baseline to compare tabular deep learning against XGBoost on this dataset. It is not part of the runtime pipeline: XGBoost proved superior on the 63-dimensional tabular representation, and the MLP remains a pedagogical artifact. It can be ignored when tracing the production data flow.

### System Workflow
1. **SMILES Resolution (`shared/pubchem_client.py`):** Resolves commercial trade names or CAS Registry Numbers (e.g., `Benzophenone` or `119-61-9`) into canonical SMILES strings via a three-tier hierarchy (Cache CSV → Curated Manual Dictionary → PubChem REST API).

2. **Image Generation (`shared/molecule_images.py`):** RDKit renders 2D molecular structures into $224 × 224$ grayscale pixel grids with 4-fold rotational augmentation (0°, 90°, 180°, 270°).

3. **Computer Vision Feature Extraction (`phase2/`):** Pass molecular images through a frozen pre-trained **MobileNetV2** backbone on ImageNet. Global Average Pooling extracts a 1280-dimensional visual embedding per image.

4. **Dimensionality Reduction & DoE Construction (`phase4/train_xgboost.py`):** Rotational augmentations are averaged per molecule. Principal Component Analysis (PCA) compresses 1280-D embeddings down to 51 components for PIs and 9 for monomers ($51 = N_{PI} − 1$, full-rank; $9 = N_{mono} − 1$). A deterministic full-factorial DoE then covers 520 PI–monomer pairs × 200 process conditions (`is_aqueous` × 10 `pi_conc` × 10 `uv_dose`) = **104,000 rows**.

5. **Physics-Informed Simulation:** Target conversion values are generated through a two-channel PI model. Channel 1 (solubility) applies a Wildman–Crippen LogP penalty in aqueous media. Channel 2 (photochemistry) multiplies the kinetic progress by the class-specific quantum efficiency $Φ_cl$: acylphosphine 0.85, benzoyl 0.60, Type II 0.45, co-initiator 0.00. These are combined with monomer reactivity, UV dose saturation, and Beer–Lambert shielding.

6. **Tabular Machine Learning (`phase4/train_xgboost.py`):** Concatenates 51 PI PCA + 9 monomer PCA + 3 process parameters (`Is_Aqueous`, `%PI`, `UV_Dose`) into a **63-dimensional** feature vector. Trains an **XGBoost Regressor** with validation-based early stopping, achieving $R^{2} = 0.978$ and $RMSE = 1.49$%.

7. **Pair-Level Compatibility Classifier (`phase4/train_compatibility_classifier.py`):** The DoE is aggregated to 1,020 unique (PI, monomer, medium) groups by taking the max conversion across all process windows. A **Random Forest** classifier predicts whether a pair can reach viable conversion (≥ 60%) under any condition; the correct question for a fast pre-screening filter. With the $Φ_cl$ physics in the target, **4107-D Morgan Fingerprints (PR-AUC 0.770)** outperform **11 physical descriptors (PR-AUC 0.739)**, demonstrating that *the molecular representation must follow the physics of the target.* Full audit in `docs/compatibility-audit.md`.

8. **Inference Pipeline & Reflex Web App (`inference/`, `app/`):** Exposes `predict()` with lazy singleton model loading (30× speedup for warm requests) and a reactive web dashboard.

---

## Technical Implementation & Pedagogical Choices

### 1. The Computer Vision Choice (Pedagogical vs. Production)
* **Educational Context:** Feeding 2D molecular structure drawings into a Convolutional Neural Network (MobileNetV2) was implemented specifically to fulfill the **Data Science specialization** requirements of the BeCode Bootcamp (**Deep Learning & Computer Vision** content).
* **Production Reflection:** In pure chemical informatics, molecular graph representations (GNNs) or direct 2D/3D QSAR descriptors are computationally more direct than image-based CNN embeddings.
* **Future Computer Vision Repurposing:** In future iterations of this project, the Computer Vision module will be repurposed for physical laboratory images (e.g., contact angle sessile drop images for surface energy, optical microscopy of printed film thickness, or SEM cross-sections), while chemical embeddings transition to direct QSAR and graph representations.

### 2. XGBoost vs. Deep Learning Neural Network
* **Phase 3 PyTorch Baseline:** A Multi-Layer Perceptron (MLP) was constructed in PyTorch as an educational baseline ($R^2 \approx 0.42 - 0.88$ depending on synthetic noise).
* **Phase 4 XGBoost Dominance:** XGBoost proved vastly superior for tabular integration of embeddings and environmental variables, capturing non-linear interactions (e.g., LogP mismatch penalties in aqueous media) and reaching $R^2 = 0.9860$ and $\text{RMSE} = 1.58\%$.

### 3. Software Engineering & MLOps Best Practices
* **Training/Inference Contract:** Identical preprocessing (4-rotation averaging and PCA transformation matrices saved via `joblib`) is applied at inference time to prevent silent feature distribution drift.
* **Import Safety & Thread Safety:** All module-level batch code is protected with `if __name__ == "__main__":`, allowing clean imports in Reflex without triggering network calls. Thread-safe atomic CSV logging uses global locks (`threading.Lock`).

---

## 📁 Repository Structure

```text
AI-Powered-UV-Curing-Predictor-and-PI-Discovery/
├── app/
│   ├── app.py
│   ├── models.py
│   ├── pages/
│   │   └── index.py
│   └── state.py
├── inference/
│   └── pipeline.py
├── phase1/
│   ├── fetch_molecules_PIs.py
│   ├── fetch_molecules_monomers.py
│   ├── generate_images_PIs.py
│   ├── generate_images_monomers.py
│   └── data/
│       ├── molecules_PIs.csv
│       ├── molecules_monomers.csv
│       ├── molecular_metadata.csv
│       ├── molecular_metadata_monomers.csv
│       └── smiles_cache_PIs.csv
├── phase2/
│   ├── extract_embeddings_PIs.py
│   ├── extract_embeddings_monomers.py
│   └── data/
│       ├── embeddings_PIs.npy
│       ├── embeddings_monomers.npy
│       └── embeddings_metadata_PIs.csv
├── phase4/
│   ├── train_xgboost.py
│   ├── pca_pi.pkl
│   ├── pca_mono.pkl
│   ├── model_config.json
│   ├── xgboost_model.json
│   └── data/
│       └── doe_dataset.csv
├── shared/
│   ├── molecule_images.py
│   ├── pubchem_client.py
│   ├── qsar_descriptors.py
│   └── utils.py
├── README.md
├── requirements-app.txt
├── requirements-training.txt
└── tests/
    └── test_qsar_simulation.py
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
**Dual-Environment Isolation:** The training pipeline and the web application are deliberately isolated into two conda environments with different Python versions (3.9 and 3.11). This resolves a hard dependency conflict: the CNN backbone requires NumPy 1.x for RDKit compatibility, while the Reflex web stack requires NumPy 2.x. Attempting to merge them into a single environment results in an irreconcilable dependency resolution failure. The dual-environment architecture mirrors the standard practice of separating offline training infrastructure from online serving infrastructure in production ML systems.
```bash
conda create -n reflex_app python=3.11 -y
conda activate reflex_app
pip install -r requirements-app.txt

# Node.js is required by Reflex to compile the frontend
conda install -c conda-forge "nodejs>=22.22" -y
```

### 4. Retrain the Model from Scratch  
Only needed if you want to regenerate xgboost_model.json, pca_pi.pkl, and pca_mono.pkl from raw data.  
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


# Phase 4: train XGBoost (PCA + DoE + early stopping)
python phase4/train_xgboost.py
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
✅ **Done:** SMARTS-based acrylate vs methacrylate detection, functionality-weighted reactivity, α-methyl steric penalty, Wildman-Crippen LogP solubility penalty, and the Φ_cl photochemical efficiency channel (4 literature-derived classes: acylphosphine 0.85, benzoyl 0.60, Type II 0.45, co-initiator 0.00).  
⬜ **Pending:** Double Bond Density (DBD) per monomer, topological polar surface area (TPSA) on the monomer side, quantum-mechanical descriptors (HOMO/LUMO energies) for radical stability.  
2. **Simulation Engine Refinements:**
    - **Hybrid lab + simulated data (`train_xgboost.py` → `simulate_target_values`):** When FTIR conversion curves become available for specific PI–monomer pairs, substitute the simulated target with the measured value instead of generating it. The pipeline is already structured to accept this without architectural change.
    - **Ink/coating thickness:** Introduce cured-film thickness as a simulation variable.It couples with the Beer–Lambert inner-filter effect and controls depth-resolved conversion, critical for 3D printing and thick adhesive layers.
    - **Multi-PI formulations:** Generalize the simulator to compute conversion for PI blends (as used in water-based ink formulations), not only single PI per formulation. Requires modeling of Type I / Type II synergy and co-initiator pairing.
    - **$α_{max}$ for monomer blends:** The current vitrification ceiling assumes a single monomer species with first-order crosslink penalty. Blends require a mixture-weighted $T_{g}$ model (Fox or Gordon–Taylor) rather than a linear crosslink counter.
    - **Configurable heuristic constants:** Revise and externalize the hardcoded coefficients in `simulate_conversion_qsar()` (`tau_dose = 250`, the 0.60 + 0.40 term, the $α_{max}$ penalties) into a versioned JSON or YAML config. This makes the simulator auditable and tunable without touching code.
    - **Additional quality metrics (post-poster):** Beyond R² and RMSE, add Spearman ρ between predicted and true conversion, calibration curves per $Φ_cl$ class, and stratified RMSE by monomer functionality. Track them in `model_training_report.md` for a richer poster-vs-paper comparison.
3. **Learned Classifiers & Representation Alternatives:**
    - **PI photochemical class classifier:** Train a model to predict the $Φ_cl$ class (acylphosphine / benzoyl / Type II / co-initiator) directly from SMILES, replacing the current literature lookup with a learned mapping. This would close the loop on "the CNN already seems to encode this information (see `Visual_47` audit)". A parallel classifier for monomer reactivity class (mono / di / tri-acrylate) is a natural companion.
    - **Morgan Fingerprints (2048-bit) + XGBoost as regression alternative:** The pair-level compatibility classifier already demonstrated that 4107-D Morgan FPs outperform 11 physical descriptors when the target includes photochemical physics (PR-AUC 0.770 vs 0.739). Evaluate whether the same holds for the regression target, as a complement (not replacement) to the CNN embedding path. The CNN remains the pedagogical anchor of the bootcamp; Morgan FP becomes a second, chemistry-native pipeline to compare.
    - **Latent factor audit: extend, don't redo:** The post-hoc audit (`docs/latent_factors_audit.md`) is complete: `Visual_0` ↔ molecular size (ρ = +0.84), `Visual_1` ↔ aromaticity (ρ = +0.51), `Visual_2` ↔ ring topology (ρ = −0.45). Conclusive separation of the acylphosphine subclass (n = 3) requires expanding the PI dataset to ≥ 20 acylphosphines; when that happens, rerun the audit as a one-line script.
4. **Dual-Model Formulation & Printing Window (`desired_prod_curing-and-formulation-prediction-pipeline.md`):**
Expanding into a dual-model system:  
    - **Model 1 (Printing/Jetting):** Predicts blend viscosity ($η_{mix}$), surface tension ($γ_{mix}$), and calculates the Ohnesorge/Z-number printability window ($1 < Z < 10$).
    - **Model 2 (Curing):** Predicts double-bond conversion and cured film $T_{g}$.
    - **Multi-Objective Optimization:** Integrating Optuna Bayesian optimization to discover optimal ink compositions.
5. **Active Learning & Generative Discovery (`post-mvp-roadmap.md`):**
    - **Active Learning:** Bayesian Optimization with Upper Confidence Bound (UCB) acquisition functions to select optimal experimental candidates.
    * **Generative Modeling:** Variational Autoencoder (VAE) on SMILES for *in-silico* generation of novel photoinitiators.
    * **Closed-Loop Discovery:** Coupling generator, predictor, and acquisition function in an automated loop.
6. **Architecture & Engineering Enhancements:**
    - **Runtime Catalogue Management - PARTIALLY IMPLEMENTED:**  
    ✅ **Done:** The molecule catalogue is fully data-driven and no longer hardcoded in Python. `data/entities.yaml` is the single source of truth for photoinitiators and monomers; `shared/entity_registry.py` loads it, exposes flat name lists (`get_pi_names`, `get_monomer_names`), and builds the manual fallback dictionary consumed by shared/pubchem_client.py. For any molecule *not* in the YAML, `pubchem_client.py` still resolves it at inference time via the three-tier hierarchy (local cache → YAML fallback → PubChem REST API). Net effect: no Python file needs editing to add a molecule; any compound PubChem knows can be predicted today.  
    ⬜ **Pending:** Two gaps remain on top of the registry. (1) **Write-back:** there is no function that promotes a successful ad-hoc PubChem lookup into a new entry of `entities.yaml` (with a stable internal name, aliases, and curated metadata), so the registry only grows by manual editing. (2) **UI:** no app-level action to add a resolved molecule to the catalogue, and no autocomplete that queries both `entities.yaml` and the live PubChem resolver.  
    The gap is between *"no hardcoded lists, everything resolvable"* (done) and *"the catalogue can grow itself from user activity"* (pending).
    - **Config externalization - PARTIALLY IMPLEMENTED (`future-refactor-externalize-config.md`):**  
    ✅ **Done:** Molecule configuration is fully externalized. `data/entities.yaml` is the versioned single source of truth for photoinitiators and monomers (names, aliases, fallback SMILES, roles); `shared/entity_registry.py` loads it and exposes flat name lists and the manual fallback dictionary. Stable, low-cardinality rules (trade-name prefixes, monomer suffix patterns, unit lists, compatibility threshold) intentionally remain in `entity_registry.py`, with a documented threshold (`> ~20 rules → move to entity_rules.yaml`). No Python file needs editing to add a molecule.  
    ⬜ **Pending:** Simulator constants are still hardcoded inside `train_xgboost.py` and should be externalized to a versioned config file (YAML or JSON) alongside entities.yaml. The set includes: `PI_EFFICIENCY_LOOKUP` (the four $Φ_cl$ values), `tau_dose`, `alpha_max` base value and per-crosslink penalty, the monomer-factor blend term `0.60 + 0.40 * (mono_factor / 1.5)`, the Beer–Lambert peak (3.0 wt%) and decay constant (2.5), the LogP solubility-penalty coefficients (25.0 / 8.0 / 2.0), and the logistic mapping parameters (midpoint 40.0, scale 12.0). Also pending: externalizing the factorial grid (`pi_conc_list`, `uv_dose_list`) so that DoE composition is reproducible from config, not from code. When done, changing a physical coefficient should not require touching Python.  
    - **SQLModel migration (rx-model-to-sqlmodel-migration-guide.md):** Migrating database models to pure SQLModel for Reflex 1.0 compatibility, with an explicit database schema design for the R&D use case (prediction history, formulation tracking, and rheology/printability records).
    - **Embedding Interpretability & Visualization — PARTIALLY IMPLEMENTED:**  
    ✅ **Done:** The sanity check on what the 1280-D embeddings capture has been performed analytically, not visually. `phase4/audit_latent_factors.py` applies PCA to the MobileNetV2 embeddings and runs two complementary tests: (1) **Spearman ρ** between each PCA component and a 16-descriptor RDKit panel, and (2) **Kruskal–Wallis** across the four $Φ_cl$ classes, with BH-FDR correction across 51 tests. Results (in `docs/latent_factors_audit.md`): 
        - `Visual_0` ↔ molecular size (ρ = +0.84 with HeavyAtoms/LabuteASA/MolMR); 
        - `Visual_1` ↔ aromaticity (ρ = +0.51 with NumAromaticRings); 
        - `Visual_2` ↔ ring topology (ρ = −0.45 with RingCount).   

        Separation of the acylphosphine subclass is inconclusive at the current dataset size (n = 3), documented as a limitation rather than hidden.   
        ⬜ **Pending (low priority):** A 2D projection (t-SNE or UMAP) of the embeddings, colored by $Φ_cl$ class and by monomer functionality, persisted to `phase2/visuals/embedding_umap.png`. Not a scientific gap: the audit already answers the underlying question, but a useful figure for presentations and a sanity check for future dataset expansions. UMAP is already a dependency (bertopic), so no new install is required.
    - **Ecosystem integration:** Synthesis-route chatbot for newly discovered PIs; linking the tool to laboratory inventory / ERP software.
7. **User Interface & UX Optimization:**  
The current Reflex interface is functional and pedagogically clear, but designed as an MVP demonstration rather than a polished end-user product. Known limitations:
    - **First-prediction latency:** ~8 s cold start while TensorFlow + MobileNetV2 + XGBoost load. Improvement: warm up lazy singletons on app startup.
    - **Minimal error feedback:** Distinguish between "molecule not found", "CAS not registered in PubChem", "invalid input", and network errors with tailored messages.
    - **No prediction history view:** Expose the curinglog table via a `/history` page with filters.
    - **No input autocomplete:** Populate a dropdown from the existing molecule CSVs; extend to dynamic entries once the catalogue is no longer hardcoded.
    - **No responsive layout:** Add `rx.desktop_only` / `rx.mobile_and_tablet` components.
    - **No dark mode toggle:** `rx.theme(appearance="light")` is hardcoded.
8. **Beyond CNN Embeddings - Graph and Transformer Architectures (Exploratory):**  
The current pipeline relies on 2D image embeddings from a pre-trained CNN. While pedagogically valuable and functionally effective, this is not the standard representation in modern cheminformatics. Future iterations may explore:
    - **Graph Neural Networks (GNNs):** PyTorch Geometric, DGL.
    - **Pre-trained Chemical Transformers:** ChemBERTa, MolFormer.
    - **Generative Molecular Architectures:** VAEs and diffusion models on SMILES for de novo photoinitiator design.
9. **Learning & Reference Material:**  
[**TeachOpenCADD**](https://github.com/volkamerlab/teachopencadd): the reference notebook series for cheminformatics + ML. Currently used as a design guide for QSAR descriptors and Morgan fingerprints; will be revisited for GNN and ChemBERTa experiments in item 8.

None of these items blocks the functional MVP, but together they represent the gap between a working prototype and a product that a formulation chemist would use daily without friction.

<br>

## Changelog

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