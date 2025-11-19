# Attention-Based Hierarchical Graph Autoencoder for Dose-Specific Single-Cell Resistance Dynamics

Code for: **"Attention-Based Hierarchical Graph Autoencoder for Dose-Specific Single-Cell Resistance Dynamics"**

Sachit Satyal and Jean Gao  
Department of Computer Science and Engineering, The University of Texas at Arlington

*Submitted to BMC Bioinformatics, 2025*

---

## Overview

This repository implements a hierarchical graph attention autoencoder that models dose-specific single-cell transcriptional responses by integrating pathway, gene, and cell hierarchies with LSTM-based dose conditioning.

**Key Features:**
- Hierarchical pathway-gene-cell architecture
- LSTM-based sequential dose encoding with virtual dose nodes
- Multi-head attention mechanisms for interpretability
- Extrapolation to unseen high doses beyond training range

**Performance:**
- Validation loss: 0.160 ± 0.045 (5-fold cross-validation)
- T320 extrapolation: cosine similarity 0.98
- Successfully predicts T640 trajectory beyond training range

---

## Repository Structure
```
.
├── src/              # Source code (models, training, analysis)    
├── DEG_Results/      # Differential expression analysis results
├── README.md         # This file
├── LICENSE           # MIT License
└── requirements.txt  # Python dependencies
```

---

## Requirements

**Hardware:**
- Minimum: 16GB RAM, 8GB GPU (NVIDIA)
- Recommended: 32GB RAM, 16GB GPU

**Software:**
- Python 3.8+
- PyTorch 2.0+
- PyTorch Geometric 2.3+
- CUDA 11.0+ (for GPU)

**Installation:**
```bash
pip install -r requirements.txt
```

---

## Data

**Dataset:** GSE206125  
Single-cell RNA-seq of BRCA2-deficient Kuramochi ovarian cancer cells exposed to escalating olaparib concentrations (T1-T320)

**Download:**
- GEO: https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE206125
- Publication: França et al., Nature 2024

**Pre-processed Data:**  
Pre-processed heterogeneous graphs and trained models available on Zenodo: [DOI to be added]

---

## Model Architecture

**Encoder:**
- Hierarchical message passing (cell → gene → pathway)
- LSTM-based dose embedding refinement
- Virtual dose node injection at all levels
- Edge-conditioned NNConv layers

**Decoder:**
- Multi-head attention reconstruction (pathway → gene → cell)
- Auxiliary resistance prediction head
- Attention-based interpretability

**Training:**
- Optimizer: Adam (lr=1e-3, weight_decay=1e-5)
- Scheduler: ReduceLROnPlateau
- Early stopping: patience=10
- Loss weights optimized via Optuna (75 trials)
- Hardware: NVIDIA H100 GPU
- Training time: 15-30 minutes per fold

---

## Key Results

**Embedding Drift Analysis:**
- Gradual increase T1→T20 (early adaptation)
- Sharp spike T40→T80 (regime transition)
- Convergence T80→T320 (stable resistance)

**Attention Analysis:**
- Prioritizes TP53, mTOR, oxidative stress pathways
- Key genes: CDKN2A, YBX1, PRDX1, KHDRBS1

**Extrapolation:**
- T320 prediction from T1-T160: cosine similarity 0.983, MSE 0.041
- T640 trajectory prediction beyond training range

**Ablation Study:**
- No virtual nodes: +95% total loss
- No attention: +77% total loss  
- No LSTM: +90% total loss

---

## Usage

See Jupyter notebooks in `src/notebooks/` for:
- Data preprocessing pipeline
- Model training and evaluation
- Visualization and interpretation

Full implementation details in paper Methods section 2.3-2.4.

---

## Citation
```bibtex
@article{satyal2025hierarchical,
  title={Attention-Based Hierarchical Graph Autoencoder for Dose-Specific 
         Single-Cell Resistance Dynamics},
  author={Satyal, Sachit and Gao, Jean},
  journal={BMC Bioinformatics},
  year={2025},
  note={Submitted}
}
```

**Dataset:**
```bibtex
@article{franca2024cellular,
  title={Cellular adaptation to cancer therapy along a resistance continuum},
  author={França, Gustavo S and others},
  journal={Nature},
  volume={631},
  pages={876--883},
  year={2024},
  doi={10.1038/s41586-024-07690-9}
}
```

---

## Contact

**Corresponding Author:** Sachit Satyal  
**Email:** sxs3757@mavs.uta.edu  
**Supervisor:** Jean Gao (gao@uta.edu)  
*

---

## Declarations

**Funding:** University of Texas at Arlington

**Data Availability:** GSE206125 (GEO acces

**Code Availability:** Will 

**Ethics:** Not applicable (publicly available secondary data)

**Competing Interes

---

## License

MIT License - See LICE

---

## Suppleme

Supplementary materials available at: https://docs.google.com/document/d/1ptkMZ5rYRW3duSDDn6g47h6IaTzsHTO7/edit

---

*Last updated: January 2025*
